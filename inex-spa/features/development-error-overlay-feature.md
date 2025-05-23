# Development Error Overlay Feature

When `DEV_MODE` is set to `true` in your environment configuration, INEX SPA provides a React-style error overlay directly in the browser.

* This feature helps catch and display unhandled PHP errors (Notices, Warnings, Fatals) and Exceptions with detailed information including the message, file, line number, and a stack trace.
* It's implemented via a combination of:
  * A PHP error handler (`core/debug/ErrorHandler.php`) that captures errors.
  * A JavaScript module (`public/JS/errorOverlay.js`) that renders the overlay.
  * CSS styles (`public/css/errorOverlay.css`) for the overlay's appearance.
* The overlay is designed to be informative and minimally intrusive, allowing for quicker debugging during development. It can be dismissed with an 'X' button or the 'Escape' key.
* **Note:** While the backend error capturing has been tested, the visual presentation and interactivity of the overlay should be confirmed in a browser environment.

\
