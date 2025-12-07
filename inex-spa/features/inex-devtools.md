---
hidden: true
---

# INEX DevTools

The INEX SPA framework includes a built-in debug bar for development environments, providing valuable insights into your application's performance and structure.

#### Features

* **Debug Bar:** A persistent bar at the bottom of the screen in development mode.
* **Performance Stats:** View execution time and memory usage for each request.
* **Database Queries:** Inspect all SQL queries executed for a page.
* **Route Information:** See details about the current route being displayed.
* **Included Files:** View a list of all PHP files included in the current request.
* **Server Information:** Inspect `$_SERVER` variables.
* **Session Data:** View the content of the `$_SESSION` superglobal.
* **Request Data:** See `$_GET`, `$_POST`, and `$_COOKIE` data.

#### Enabling and Using DevTools

The DevTools are controlled by an environment variable in your `.env` file:

* `DEV_MODE`: Set to `true` to enable the debug bar. Set to `false` or remove the line for production environments.

Example `.env` entry:

```ini
DEV_MODE=true
```

Once enabled, the DevTools bar will appear at the bottom of your screen. You can use the following keyboard shortcut to toggle its visibility:

* **`Ctrl + D`**: Show or hide the DevTools bar.

You can click on the tabs to navigate between different panels.
