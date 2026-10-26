# Equatistry

An interactive mathematical art studio built with JavaScript, WebGL, and GLSL. Type an expression to change an animated fragment shader, combine presets, and adjust a three-color palette.

![Example visualization](example%201.png)

## Run locally

Clone this repository and serve it with Python 3:

```sh
git clone https://github.com/CodeOnWheels/Equatistry.git
cd Equatistry
python -m http.server 8000
```

Open http://localhost:8000 in a browser with WebGL support. No package installation or build step is required.

## Explore

- Edit the equation at the top of the screen. Manual edits make the displayed expression your new base and clear preset selections.
- Combine the Fibonacci Spiral, Hyperspace, Neon Vortex, and Digital Noise presets.
- Adjust Core, Mid, and Glow colors.
- Use Hide HUD or press Space outside an input to toggle controls. Move the mouse to reveal the toggle again.
- Clear All resets the equation and selected presets.

## How it works

The equation is inserted into a fragment shader and compiled at runtime. Each pixel receives a value derived from the expression; its magnitude is clamped to a color palette. Animation uses `requestAnimationFrame`.

Available variables include `uv` (normalized pixel position), `x` and `y` (pixel coordinates), `res` (canvas dimensions), and `t` (elapsed seconds). Expressions use GLSL syntax, including floating-point literals such as `2.0`.

Try:

```glsl
sin(uv.x * 20.0 + t)
```

## Current limitations

Invalid equations display an error while the last valid visualization continues. Shader compile/link results are checked before replacing the active program, and replaced resources are released. If WebGL is unavailable, the page explains how to proceed.

The interface is designed primarily for desktop use. WebGL availability and shader precision vary by device. There is no image-export control.

