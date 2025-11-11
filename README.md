## AZ Animations (AZ-animation)

Lightweight, class-based animation utilities. This folder contains only the animation runtime and related classes. Use it to add ready-made animations via HTML classnames, with optional duration, delay, and repeat modifiers.

-----

### Files in this folder

- `az_anims.js`: Minified/compact runtime. Uses classnames without underscores for modifiers, e.g. `dur11`, `delay2`, `rpt3` or `repeat3`.
- `main.js`: Readable runtime. Uses underscore-based modifiers, e.g. `dur_1.5`, `delay_2`, `repeat_3`. Functionally similar to `az_anims.js` but different classname formats.

Use one runtime at a time. Prefer `az_anims.js` in production for smaller size; `main.js` is helpful for readability/debugging.

-----

### Include and initialize

Add the script to your page and instantiate the runtime once after the DOM is ready.

```html
<!-- Option A: Compact runtime (no-underscore modifiers) -->
<script src="./AZ-animation/az_anims.js"></script>
<script>
  // Initializes styles, keyframes, and dynamic modifier classes
  new AzAnim();
</script>

<!-- Option B: Readable runtime (underscore modifiers) -->
<!-- <script src="./AZ-animation/main.js"></script>
<script>
  new AzAnimator();
</script> -->
```

Notes:
- Both runtimes inject a `<style id="az_anim_style">` with base rules and keyframes.
- Base CSS variables: `--dur` (default 1s), `--delay` (default 1s), `--repeat` (default 1).

-----

### Core classes

- `az_anim`: Apply an animation immediately.
- `az_anim_hov`: Only apply animation on hover (use with an animation name).
- `infinite`: Force infinite looping (overrides repeat).
- `az_anim_paused`: Pause an ongoing animation (toggle-able).

Usage example:
```html
<!-- Plays immediately -->
<div class="az_anim bounce dur11"></div>

<!-- Plays only on hover -->
<div class="az_anim_hov swing dur20"></div>
```

If you use `main.js`, the same examples would be:
```html
<div class="az_anim bounce dur_1.1"></div>
<div class="az_anim_hov swing dur_2"></div>
```

-----

### Animation types

Apply any one (or more) of these to your element together with `az_anim` or `az_anim_hov`:

- Attention: `cube_rotate`, `blink_txt`, `blink_bg`, `blink_b_shadow`, `blink_brdr_r`, `bounce`, `flash`, `pulse`, `rubberBand`, `shakeX`, `shakeY`, `headShake`, `swing`, `tada`, `wobble`, `jello`, `heartBeat`, `beatFade`
- Back entrances/outs: `backInDown`, `backInLeft`, `backInRight`, `backInUp`, `backOutDown`, `backOutLeft`, `backOutRight`, `backOutUp`
- Bounce in/outs: `bounceIn`, `bounceInDown`, `bounceInLeft`, `bounceInRight`, `bounceInUp`, `bounceOut`, `bounceOutDown`, `bounceOutLeft`, `bounceOutRight`, `bounceOutUp`
- Fades: `fadeIn`, `fadeInDown`, `fadeInDownBig`, `fadeInLeft`, `fadeInLeftBig`, `fadeInRight`, `fadeInRightBig`, `fadeInUp`, `fadeInUpBig`, `fadeInTopLeft`, `fadeInTopRight`, `fadeInBottomLeft`, `fadeInBottomRight`, `fadeOut`, `fadeOutDown`, `fadeOutDownBig`, `fadeOutLeft`, `fadeOutLeftBig`, `fadeOutRight`, `fadeOutRightBig`, `fadeOutUp`, `fadeOutUpBig`, `fadeOutTopLeft`, `fadeOutTopRight`, `fadeOutBottomRight`, `fadeOutBottomLeft`
- Flip: `flip`, `flipInX`, `flipInY`, `flipOutX`, `flipOutY`
- LightSpeed: `lightSpeedInRight`, `lightSpeedInLeft`, `lightSpeedOutRight`, `lightSpeedOutLeft`
- Rotate in/outs: `rotateIn`, `rotateInDownLeft`, `rotateInDownRight`, `rotateInUpLeft`, `rotateInUpRight`, `rotateOut`, `rotateOutDownLeft`, `rotateOutDownRight`, `rotateOutUpLeft`, `rotateOutUpRight`
- Special: `hinge`, `jackInTheBox`, `rollIn`, `rollOut`
- Zoom in/outs: `zoomIn`, `zoomInDown`, `zoomInLeft`, `zoomInRight`, `zoomInUp`, `zoomOut`, `zoomOutDown`, `zoomOutLeft`, `zoomOutRight`, `zoomOutUp`
- Slide in/outs: `slideInDown`, `slideInLeft`, `slideInRight`, `slideInUp`, `slideOutDown`, `slideOutLeft`, `slideOutRight`, `slideOutUp`, `slideThroughLeft`, `slideThroughRight`, `slideThroughUp`, `slideThroughDown`
- Scale: `scaleIn`
- Gradient/visual: `gradientShift`, `fadeEffect` (main.js), `spin`, `spinConicGrad`, `loadingDots`

-----

### Duration, delay, and repeat modifiers

There are two modifier syntaxes depending on which runtime you include.

1) If you use `az_anims.js` (no underscores):
- `dur{n}`: Duration accepts up to 30 seconds. Values are provided as seconds/10.
  - Examples: `dur1` = 0.1s (minimum), `dur11` = 1.1s, `dur300` = 30s (maximum).
- `delay{n}`: Delay in whole seconds from 1 to 30.
  - Examples: `delay1` = 1s, `delay10` = 10s, `delay30` = 30s.
- `rpt{n}` or `repeat{n}`: Repeat count from 1 to 30.
  - Examples: `rpt1` (play once), `rpt3` (3 times), `repeat10` (10 times).
- `infinite`: loop forever.

2) If you use `main.js` (underscore syntax):
- `dur_{n}` or `speed_{n}`: Multiplier of the base `--dur` (default 1s). Commonly pass real seconds like `dur_1.1` (1.1s) or `dur_2` (2s).
- `delay_{n}`: Delay in seconds (supports decimals), e.g. `delay_1`, `delay_2.5`.
- `repeat_{n}`: Repeat count, e.g. `repeat_1`, `repeat_10`.
- `infinite`: loop forever.

Important:
- Base variables can be customized globally: `:root { --dur: 1s; --delay: 1s; --repeat: 1 }`.
- For `az_anims.js`, `dur{n}` maps `n` → seconds/10 to cap at 30 seconds: `1 → 0.1s`, `11 → 1.1s`, `300 → 30s`. `delay` and `rpt/repeat` accept normal integer values from 1 to 30.

-----

### Practical examples

```html
<!-- Bounce forever with a 1.1s cycle -->
<div class="az_anim bounce infinite dur11"></div>

<!-- Fade in, delay 2s, play 3 times -->
<div class="az_anim fadeIn delay2 rpt3 dur20"></div>

<!-- Hover-only wobble with short duration -->
<button class="az_anim_hov wobble dur5">Hover me</button>
```

Using `main.js` equivalents:
```html
<div class="az_anim bounce infinite dur_1.1"></div>
<div class="az_anim fadeIn delay_2 repeat_3 dur_2"></div>
<button class="az_anim_hov wobble dur_0.5">Hover me</button>
```

-----

### Tips

- Combine one or more animation names with the base class: `az_anim fadeInUp`, `az_anim_hov shakeX`.
- Use `az_anim_paused` to pause/resume via JS by toggling the class.
- Prefer `az_anims.js` for production (smaller), `main.js` when you need explicit underscore-based modifiers or easier debugging.


