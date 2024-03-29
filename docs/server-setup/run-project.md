# Run your Project

`pm2` is a great tool for managing applications. Install it with:

```bash
npm install -g pm2
```

Then create a new `pm2` process for your application with:

```bash
pm2 start 'script' --name 'app-name'
```

Note that you will replace `script` (keep the quotes!) with the script you use to start your application (such as `npm start` or `npm run develop`), and replace `app-name` with a user friendly name for your application.

For example:

```bash
pm2 start 'npm start' --name 'BeccaLyria'
```

## Maintaining Your Applications

On occasion you will need to perform maintenance on your droplet. You will want to SSH into your droplet, then run `reboot` to restart the system. This will kick you off the SSH connection, and you will not be able to reconnect until the reboot is complete.

Once this is done, you can restart your `pm2` process with `pm2 resurrect`.

A few helpful `pm2` commands:

- `pm2 ls`: Lists all `pm2` processes, including helpful information such as the status (running or stopped), name, PID, and number of times it has been restarted.
- `pm2 restart <name>`: Restarts the process with the given name (you can use the PID instead).
- `pm2 stop <name>`: Stops the process with the given name.
- `pm2 delete <name>`: Removes the process with the given name.
- `pm2 logs <name>`: Displays the logs for the process' application.
- `pm2 save`: Saves your current list of running processes (pairs with the `resurrect` command)
