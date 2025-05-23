# CronJob Feature

INEX SPA allows you to define and manage scheduled tasks or cron jobs using Ammar CLI. These jobs are PHP classes stored in the `core/cronjobs/` directory. Each job file should be named after the class it contains (e.g., `MyTask.php` for class `MyTask`). Each class must define a public `execute()` method, which contains the logic for the job.

Available commands:

*   **Create a new cron job:**

    ```bash
    php ammar make:cronjob -1 YourJobClassName
    ```

    This will create a new file `core/cronjobs/YourJobClassName.php` with the following basic structure:

    ```php
    <?php

    class YourJobClassName {
        /**
         * The main logic for the cron job.
         */
        public function execute() {
            // Your cron job logic here
            echo "Cron job 'YourJobClassName' executed at " . date('Y-m-d H:i:s') . "\n";
        }
    }
    ```
*   **List all cron jobs:**

    ```bash
    php ammar list:cronjobs
    ```

    This command displays all available cron jobs.
*   **Run a cron job manually:**

    ```bash
    php ammar run:cronjob -1 YourJobClassName
    ```

    This is useful for testing your cron job logic.
*   **Delete a cron job:**

    ```bash
    php ammar delete:cronjob -1 YourJobClassName
    ```

    This will remove the specified cron job file.

**Note:** The actual scheduling of these cron jobs (e.g., running them at specific times) needs to be configured separately using your server's cron facilities (like `crontab` on Linux) to call the `php ammar run:cronjob -1 YourJobClassName` command.
