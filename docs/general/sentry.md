# Sentry

Sentry is an external logging tool (with a substantially featured free-tier) for capturing exceptions and logging stack traces.

## Node-TS Configuration

This configuration is for a Node.js and TypeScript project, following [my standard configuration](/node-ts-config/index.md).

Install the requisite packages with:

```bash
npm i @sentry/node @sentry/integrations
```

Then, in the entry point file (usually `src/index.ts`), add the initialisation code.

```ts
import { RewriteFrames } from "@sentry/integrations";
import * as Sentry from "@sentry/node";

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  tracesSampleRate: 1.0,
  integrations: [
    new RewriteFrames({
      root: global.__dirname,
    }),
  ],
});
```

- `dsn`: This is obtained from the Sentry dashboard when you set up your project, and tells the code where to send the errors. You should keep this within an `.env` file, as `SENTRY_DSN`, to ensure no one sends false notifications to your dashboard.
- `tracesSampleRate`: This sets how often Sentry should log errors. Here we've told it to capture 100% of the errors.
- `integrations`: The `RewriteFrames` tool is used to help map the errors to the compiled JavaScript code and prevent things from getting lost.

Now set up a global error handler in `src/utils/errorHandler.ts`:

```ts
import * as Sentry from "@sentry/node";

import { logHandler } from "./logHandler";

/**
 * Standard error handling module to pipe errors to Sentry and
 * format the error for logging.
 *
 * @param {string} context A description of where the error occurred.
 * @param {Error} error The error object.
 */
export const errorHandler = (context: string, error: Error): void => {
  logHandler.log("error", `There was an error in the ${context}:`);
  logHandler.log(
    "error",
    JSON.stringify({ errorMessage: error.message, errorStack: error.stack })
  );
  Sentry.captureException(error);
};

```

Note that the `logHandler` comes from our [Winston configuration](/general/winston.md). These two tools pair very well together. If you aren't using winston, you can replace the `logHandler` with a standard `console.log`.

## Angular Configuration

The configuration for a front-end Angular application is a bit different.

First, install the needed packages:

```bash
npm i @sentry/angular @sentry/tracing
```

Then, in the `src/main.ts` file, add:

```ts
import * as Sentry from "@sentry/angular";
import { Integrations } from "@sentry/tracing";

Sentry.init({
  dsn: "actual dsn here!",
  integrations: [
    new Integrations.BrowserTracing({
      tracingOrigins: ["localhost", "https://leaderboard.nhcarrigan.com"],
      routingInstrumentation: Sentry.routingInstrumentation,
    }),
  ],
  tracesSampleRate: 1.0,
});
```

Note that unlike above, you'll need to hard-code your DSN value. This is safe, according to Sentry, though we recommend setting the project configuration to only accept data from your live url (just in case).

Finally, to tie Sentry in to Angular's built-in error handling, add this to your `src/app/app.module.ts` code:

```ts
import { APP_INITIALIZER, ErrorHandler, NgModule } from '@angular/core';
import * as Sentry from '@sentry/angular';

 providers: [
    {
      provide: ErrorHandler,
      useValue: Sentry.createErrorHandler({
        showDialog: true,
      }),
    },
    {
      provide: Sentry.TraceService,
      deps: [Router],
    },
    {
      provide: APP_INITIALIZER,
      useFactory: () => () => {},
      deps: [Sentry.TraceService],
      multi: true,
    },
  ],
```

Note that this does assume you are using Angular Router (which, you probably are.)
