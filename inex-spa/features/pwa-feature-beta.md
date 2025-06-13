# PWA Feature (Beta)

Our Framework Support `Progressive Web App (PWA)` Feature

## Enable It

### Update .env

Update .env by set `USE_PWA` to true:

```ini
USE_PWA=true
```

## Setup it

### Update public/manifest.json

Go to `public/manifest.json` file to set Some things for `PWA` , you will see like this:

```json
{
  "name": "MyApp",
  "short_name": "MyApp",
  "start_url": "/index.html",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#3367D6",
  "icons": [
    {
      "src": "/images/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/images/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

#### Set Variables

`name`: For Application Name.

`short_name`: For Short name from Application Name.

`start_url`: This is the link will be open when click on Application.

`display`: For how to display Application when open.

`background_color`: This is the background color for Application.

`theme_color`: This is for The theme color of Application.

`icons`: Add your all application size icons and upload icons to `public` folder.

### Update public/manifest\_config.html

Go to `public/manifest_config.html` and update the `<head>` code. and add all icons like this:

```html
<link rel="manifest" href="/manifest.json">
<meta name="theme-color" content="#3367D6">
<!-- Optional: Apple touch icons for iOS -->
<link rel="apple-touch-icon" href="/images/icon-192x192.png">
<!-- ...other sizes... -->
<meta name="apple-mobile-web-app-status-bar" content="#3367D6">
```

### Update public/offline.html

Go to `public/offline.html` and set code for What's will do if User open Application and he's offline. like this:

```html
You are offline. Please check your internet connection and try again.
<script>
  // This script checks if the user is online or offline
  window.addEventListener('offline', function() {
    document.body.innerHTML = 'You are offline. Please check your internet connection and try again.';
  });

  window.addEventListener('online', function() {
    document.body.innerHTML = 'You are back online!';
    setTimeout(() => {
      window.location.reload();
    }, 5000);
  });
</script>
```

### Update public/service-worker.js

Go to `public/service-worker.js` and update this section of top of the file for any static files:

```javascript
const CACHE_NAME = 'myapp-v1';
const URLS_TO_CACHE = [
  '/',
  '/index.php',
  '/styles/main.css',
  '/scripts/app.js',
  '/images/icon-192x192.png',
  '/images/icon-512x512.png',
  '/offline.html'
  // add other static assets
];
```

#### Set Vairables

`CACHE_NAME`: For Cache Version or name.

`URLS_TO_CACHE`: This is all static files you want to save in user storage to work if application offline.

#### Edit Offline URL

You can edit what's page will show if user open Application and he's offline in this way, too (Way 2) (Advanced) (Not Recommended) by this 54 line in file:

```javascript
return caches.match('/offline.html');
```

## Enable SSL

Your Website should have `SSL` to `PWA Feature` work.

{% hint style="info" %}
Search online for more information
{% endhint %}

## Notes

1- Website should have `SSL`

2- This feature in `Beta` Version and may have errors

3- Should include the `Offline` and `Offline Static Assets` in `URLS_TO_CACHE`.

4- When you create a new cache version, rename it.
