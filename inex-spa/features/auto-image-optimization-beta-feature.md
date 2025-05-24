# Auto Image Optimization (Beta) Feature

Provides an `image()` helper function (`core/functions/PHP/image.php`) for on-the-fly client-side image processing.

**Status:** This feature is currently in **Beta**.

**Activation:** To enable this feature, set the `USE_IMAGE_OPTIMIZATION_BETA=true` variable in your `.env` file. If `false` or not set, a standard `<img>` tag is rendered without client-side processing.

**Function Signature:**

```
image(string $src, string $alt = '', ?int $width = null, ?int $height = null, float $quality = 0.8, string $format = 'webp', array $attributes = [])
```

**Parameters:**

* `$src` (string): Path or URL to the original image.
* `$alt` (string, optional): Alt text for the image.
* `$width` (int, optional): Desired output width. If null, original width or aspect ratio is maintained.
* `$height` (int, optional): Desired output height. If null, original height or aspect ratio is maintained.
* `$quality` (float, optional): Compression quality for JPEG/WebP (0.0 to 1.0). Default is `0.8`.
* `$format` (string, optional): Target image format. Supports `'webp'`, `'jpeg'`, `'png'`. Default is `'webp'`.
* `$attributes` (array, optional): Additional HTML attributes for the `<img>` tag (e.g., `['class' => 'my-image']`).

**Processing:** Uses `Compressor.js` library for client-side operations. The library is dynamically loaded if not already present.

**Supported Output Formats:** WebP, JPEG, PNG.

* **Limitation:** AVIF format is not currently supported due to limitations in the underlying `Compressor.js` library.

**Fallback:** If client-side processing fails or if the browser does not support the target format (e.g., WebP), the original image specified in `$src` will be displayed.

**Example Usage:**

```
// Optimize and convert to WebP, resize to 300px width (auto height)
echo image('path/to/your/image.jpg', 'My optimized image', 300);

// Convert to JPEG, quality 0.7, set specific class
echo image('path/to/another/image.png', 'Another image', null, null, 0.7, 'jpeg', ['class' => 'custom-class']);
```
