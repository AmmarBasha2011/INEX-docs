# Cronjob Management

This application includes a cronjob management system to schedule and run background tasks. Tasks are defined as PHP classes and can be managed using the `ammar` CLI.

#### Cron Runner

The core script for executing cron tasks is `core/cron/cron_runner.php`. This script is designed to be called by your system's cron daemon (e.g., crontab).

**Usage:**

```sh
/usr/bin/php /path/to/your/project/core/cron/cron_runner.php <TaskName> >> /path/to/your/project/core/logs/cron.log 2>&1
```

* Replace `/usr/bin/php` with the actual path to your PHP interpreter if different.
* Replace `/path/to/your/project/` with the absolute path to your application's root directory.
* `<TaskName>` is the name of the cron task class you want to run (e.g., `ExampleTask`).
* It's recommended to redirect output to the `core/logs/cron.log` file for monitoring.

#### `ammar` CLI Commands for Cronjobs



The `ammar` CLI tool provides several commands to help manage your cron tasks:

**1. `list:cron`**

Lists all available cron tasks. These are the `.php` files found in the `core/cron/tasks/` directory.

**Usage:**

```sh
php ammar list:cron
```

**2. `make:cron <TaskName>`**

Creates a new cron task file in `core/cron/tasks/`. The `<TaskName>` should be a valid PHP class name (e.g., `MyDailyReport`).

**Usage:**

```sh
php ammar make:cron MyDailyReport
```

This will generate `core/cron/tasks/MyDailyReport.php` with a template class structure. You'll need to edit this file to implement the task's logic within the `handle()` method.

**3. `run:cron <TaskName>`**

Manually triggers a specific cron task. This is useful for testing your cron tasks without waiting for the scheduled time.

**Usage:**

```sh
php ammar run:cron <TaskName>
```

Example:

```sh
php ammar run:cron ExampleTask
```

**4. `delete:cron <TaskName>`**

Deletes a specific cron task file from `core/cron/tasks/`. You will be prompted for confirmation.

**Usage:**

```sh
php ammar delete:cron <TaskName>
```

**5. `clear:cron`**

Deletes ALL cron task files from `core/cron/tasks/`. This is a destructive operation and will require double confirmation.

**Usage:**

```sh
php ammar clear:cron
```

#### Creating a New Cron Task



1.  Use the `make:cron` command to generate the task file:

    ```sh
    php ammar make:cron YourNewTaskName
    ```
2. Open the generated file `core/cron/tasks/YourNewTaskName.php`.
3. Implement your task's logic within the `handle()` method of the class. You can use any PHP code, access your application's models, services, or other functions as needed. Ensure necessary classes and functions are loaded, potentially by referencing how `core/cron/cron_runner.php` or `index.php` load dependencies. The `cron_runner.php` should provide a basic environment, but complex tasks might need to ensure their specific dependencies are met.
4. Test your task using `php ammar run:cron YourNewTaskName`.
5. Once ready, schedule it via your system's crontab by pointing to `core/cron/cron_runner.php YourNewTaskName`.
