# ESLint Configuration

This is my configuration for the ESLint plugin. This goes in a `.eslintrc.json` file in your project's root directory.

```json
{
  "env": {
    "es2020": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended",
    "plugin:jsdoc/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 11,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint", "jsdoc", "import", "no-only-tests"],
  "rules": {
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "double", { "allowTemplateLiterals": true }],
    "semi": ["error", "always"],
    "prefer-const": "error",
    "eqeqeq": ["error", "always"],
    "curly": ["error"],
    "require-atomic-updates": ["error"],
    "no-var": ["error"],
    "camelcase": ["error"],
    "init-declarations": ["error", "always"],
    "require-await": ["error"],
    "no-param-reassign": ["error"],
    "jsdoc/require-jsdoc": [
      "error",
      {
        "require": {
          "ArrowFunctionExpression": true,
          "ClassDeclaration": true,
          "ClassExpression": true,
          "FunctionDeclaration": true,
          "FunctionExpression": true,
          "MethodDefinition": true
        },
        "publicOnly": true
      }
    ],
    "jsdoc/require-description-complete-sentence": "error",
    "import/first": "error",
    "import/exports-last": "error",
    "import/newline-after-import": "error",
    "import/order": [
      "error",
      {
        "groups": [
          "builtin",
          "external",
          "internal",
          "parent",
          "sibling",
          "index",
          "object",
          "type",
          "unknown"
        ],
        "newlines-between": "always",
        "alphabetize": {
          "order": "asc",
          "caseInsensitive": true
        }
      }
    ],
    "no-only-tests/no-only-tests": "error"
  }
}
```

Most of the settings are required to make ESLint work correctly with Prettier and TypeScript. The rules can be modified, however.

## Rules

- `linebreak-style`: This rule throws an error if the line endings do not use Unix characters (`\n`). Windows uses `\r\n`, which this rule will prevent.
- `quotes`: This rule requires the use of double quotes for strings. Adding the `allowTemplateLiterals` option permits the use of backticks for template strings.
- `semi`: This rule expects EOL semi-colons.
- `prefer-const`: This rule will throw an error if a variable is declared with `let` but never reassigned. These variables should be declared with `const` instead.
- `eqeqeq`: This rule throws an error on any loose equality (`==`) or loose inequality (`!=`) comparisons.
- `curly`: This rule throws an error on single-line if conditions, expecting the use of curly brackets for maintainability.
