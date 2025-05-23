# make:cronjob

```bash
php ammar make:cronjob -1 YourJobClassName
```

This will create a new file `core/cronjobs/YourJobClassName.php` with the following basic structure:

````php
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
````
