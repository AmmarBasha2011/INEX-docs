# Built-in Motion Engine Feature

The framework includes a tiny helper to add simple CSS-based animations to HTML elements.

#### Enabling/Disabling the Engine

The Motion Engine can be enabled or disabled via an environment setting. In your `.env` file, add or modify the following line:

```
MOTION_ENGINE_ENABLED=true
```

Setting it to `true` enables the engine; `false` disables it. If disabled, calls to the `animate()` function will do nothing.

#### Usage

To apply an animation, use the `animate()` PHP function:

```
animate($elementSelectorOrId, $animationName, $durationMs);
```

**Parameters:**

* `$elementSelectorOrId` (string): A CSS selector (e.g., `#myElement`, `.my-class`) or a plain ID (e.g., `myElement` which will be treated as `#myElement`) for the HTML element you want to animate.
* `$animationName` (string): The name of the animation to apply. Currently, `fade-in` is a primary example. This corresponds to a CSS class `motion-<animationName>` (e.g., `motion-fade-in`).
* `$durationMs` (int): The duration of the animation in milliseconds (e.g., `500` for 0.5 seconds).

**Example:**

```
// In your .ahmed.php file or any PHP script:
animate('#myDiv', 'fade-in', 700); // Fades in #myDiv over 0.7 seconds
```

This will add the necessary CSS classes to the element and set its animation duration.

#### How it Works

The `animate()` function injects a small JavaScript snippet that:

1. Selects the target element.
2. Sets its `animation-duration`.
3. Adds two CSS classes: `motion-animate` (a base class for animations) and `motion-<animationName>` (e.g., `motion-fade-in`).

The actual animations are defined in `public/css/motion-animations.css`. A helper script at `public/JS/motion_engine.js` listens for the `animationend` event to clean up these classes from the element, allowing animations to be re-triggered if `animate()` is called again on the same element.

#### Adding New Animations

1.  **Define CSS Keyframes**: Add your `@keyframes` to `public/css/motion-animations.css`.

    ```
    @keyframes newAnimation { /* ... your keyframes ... */ }
    ```
2.  **Create Animation Class**: In the same CSS file, add a class that uses your animation.

    ```
    .motion-new-animation {
        animation-name: newAnimation;
        /* other animation properties if needed */
    }
    ```
3. **Use it**: You can then call `animate('#myElement', 'new-animation', 1000);`
