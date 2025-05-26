# Built-in Motion Engine (Beta)

**Note:** This feature is currently in Beta. While functional, it may undergo changes, and we appreciate any feedback!

This framework includes a lightweight, dependency-free JavaScript motion engine to apply CSS animations to HTML elements.

#### Enabling the Engine



The Motion Engine is controlled via an environment variable in your `.env` file:

* `USE_ANIMATE`: Set to `true` to enable the engine (default) or `false` to disable it. When enabled, the necessary JavaScript (`public/JS/motion_engine.js`) and CSS (`public/css/motion-animations.css`) files are automatically included in your pages.

Example `.env` entry:

```ini
USE_ANIMATE=true
```

#### Using the `animate` function



The core of the engine is the `animate()` JavaScript function.

**Syntax:** `animate(elementOrSelector, animationName, durationMs)`

* `elementOrSelector`: Can be either an HTMLElement object or a CSS selector string (e.g., `'#myElement'`, `'.my-class'`).
* `animationName`: A string representing the name of the animation to apply (e.g., `'fade-in'`). This corresponds to a CSS class `motion-{animationName}` defined in `public/css/motion-animations.css`.
* `durationMs`: An integer specifying the animation duration in milliseconds (e.g., `300`).

**Example Usage:**

```html
<div id="myBox">Hello!</div>

<script>
  // Get the element
  const box = document.getElementById('myBox');

  // Animate it with 'fade-in' over 300ms
  animate(box, 'fade-in', 300);

  // Or using a selector
  // animate('#myBox', 'fade-in', 300);
</script>
```

The function handles adding and removing the necessary CSS classes and setting the animation duration.

#### Adding New Animations



To add new animations:

1.  **Define Keyframes**: Open `public/css/motion-animations.css` and define your `@keyframes`. It's recommended to prefix them with `motion-` for clarity.

    ```css
    @keyframes motion-slide-up {
      from {
        transform: translateY(20px);
        opacity: 0;
      }
      to {
        transform: translateY(0);
        opacity: 1;
      }
    }
    ```
2.  **Create Animation Class**: Add a corresponding CSS class that applies these keyframes.

    ```css
    .motion-slide-up {
      animation-name: motion-slide-up;
    }
    ```

    The base class `.motion-animate` (which includes `animation-fill-mode: forwards;`) will be automatically applied by the `animate` function.
3.  **Use in JavaScript**: You can now use `'slide-up'` as the `animationName` in the `animate` function:

    ```javascript
    animate('#anotherElement', 'slide-up', 500);
    ```
