# API Routes

Now, API Routes has been released.

## Why Use It?

You can use API Routes for API and BackEnd of website. because our Framework parse his JS Files into it

## Example

### Create web/test\_request\_GET.ahmed.php

```bash
php ammar make:route
```

Then Select

* 1- test
* 2- no
* 3- GET
* no

This will be create a `RequestType` Route (normally)

* Add this code into this file

```php
<?php
// web/test_request_GET.ahmed.php
// Set the content type to application/json
header('Content-Type: application/json');

// Define your data
$data = ["ammar" => 24];

// Return it as JSON
echo json_encode($data);
```

Now, when you open in browser or fetch, you will be see like this in response:

```html
<script src='http://localhost/JS/getWEBSITEURLValue.js'></script>
<link rel='stylesheet' href='http://localhost/errors/notification.css'/>
<script src='http://localhost/JS/redirect.js'></script>
<script src='http://localhost/JS/popstate.js'></script>
<script src='http://localhost/JS/submitData.js'></script>
<script src='http://localhost/JS/csrfToken.js'></script>
<script src='http://localhost/JS/submitDataWR.js'></script>
<script src='http://localhost/JS/addAppNametoHTML.js'></script>
<script src='http://localhost/JS/showNotification.js'></script>
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>{"ammar":24}
```

Because this is thinking this is a normal page but when use API Routes.

### Create web/test\_request\_GET\_api.ahmed.php

```bash
php ammar make:route
```

Then Select

* 1- test2
* 2- no
* 3- GET
* yes

This will be create a `RequestTypeAPI` Route

* Add this code into this file

```php
<?php
// web/test2_request_GET_api.ahmed.php
// Set the content type to application/json
header('Content-Type: application/json');

// Define your data
$data = ["ammar" => 24];

// Return it as JSON
echo json_encode($data);
```

Now, when you open in browser or fetch, you will be see like this in response:

```html
{"ammar":24}
```

Because Now, this is know this is API Page.
