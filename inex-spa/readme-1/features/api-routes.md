# API Routes

## RequestTypeAPI Routes

The INEX SPA framework now supports **RequestTypeAPI Routes**, a specialized form of API routing optimized for clean and lightweight API responses without loading additional JavaScript resources. This feature is ideal for building APIs and backend services efficiently within your INEX SPA application.

***

### 🚀 Why Use RequestTypeAPI Routes?

By default, standard route files in INEX SPA load several JavaScript and CSS assets automatically to support frontend functionality. While this is great for full pages, it's unnecessary for API responses, where clean JSON output is expected.

**RequestTypeAPI Routes** solve this by:

* Disabling the automatic loading of JS/CSS assets.
* Returning pure JSON responses.
* Enhancing performance for frontend consumers (AJAX, Fetch API, mobile apps, etc).

***

### 📂 File Naming Convention

RequestTypeAPI Route files follow this pattern:

```
[route]_request_[METHOD]_api.ahmed.php
```

Where:

* `[route]` is your route name (e.g., `test2`).
* `[METHOD]` is the HTTP method (`GET`, `POST`, etc).
* The `_api` suffix distinguishes it from standard `RequestType` routes.

***

### ✨ Creating a RequestTypeAPI Route

You can easily generate a RequestTypeAPI route using the CLI command:

```bash
php ammar make:route
```

Then follow the prompts:

1. **Enter the route name:** `test2`
2. **Is it dynamic?** `no`
3. **Select request type:** `GET`
4. **Is this an API Route?** `yes`

This will create a file named:

```
web/test2_request_GET_api.ahmed.php
```

***

### 🧑‍💻 Example Code

Edit the generated file and add the following:

```php
<?php
// web/test2_request_GET_api.ahmed.php

// Set the content type to application/json
header('Content-Type: application/json');

// Define your API data
$data = ["ammar" => 24];

// Output as JSON
echo json_encode($data);
```

***

### 📊 Response Comparison

#### 🧪 Standard RequestType Route:

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

#### ✅ RequestTypeAPI Route:

```json
{"ammar":24}
```

***

### 📘 Summary

**RequestTypeAPI Routes** provide a clean, minimal, and efficient way to build APIs inside INEX SPA. They are especially useful for frontend frameworks, mobile apps, and AJAX calls where only the raw data is needed without additional JS dependencies.

Make sure to use the `_api` suffix in your route file name to activate this mode.

***

Happy Coding with INEX SPA! ⚡
