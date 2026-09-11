# TwistRot Example Files

This directory contains example files for use with the "TwistRot" feature in DevFoam.

## Files

### `revolution_vase.dat`
This file defines a **Revolution Curve**. It represents the profile of a vase.
- **Usage**: Load this as the "Revolution curve" to define the side profile of the object.
- **Format**: Simple X Y coordinates defining the profile path.

### `rotation_star.dat`
This file defines a **Rotation Curve**. It represents a star shape.
- **Usage**: Load this as the "Rotation curve" to define how the object's shape changes as it rotates. Instead of a simple circle, the object will have a star-shaped cross-section.
- **Format**: Simple X Y coordinates defining a closed loop.

### `twist_linear.dat`
This file defines a **Twist Curve**.
- **Usage**: Load this as the "Twist curve" to apply a twist to the object along its height.
- **Format**: X Y coordinates where X likely represents the height (or percentage of height) and Y represents the twist angle in degrees.

### `revolution_chubby_fish.dat`
This file defines a **Revolution Curve** for the fish ornament thickness profile.
- **Usage**: Load this as the "Revolution curve" to make the fish thin at the nose and tail, fuller through the middle, and slightly taller overall than the vase sample.
- **Point layout**: Open polyline, sorted bottom-to-top, with the largest radius around the middle of the body.

### `rotation_fish_body.dat`
This file defines a **Rotation Curve** for the fish silhouette.
- **Usage**: Load this as the "Rotation curve" to get the readable fish outline: rounded nose, fuller body, small fin bumps, and a forked tail.
- **Point layout**: Closed polyline that starts at the nose, walks along the top edge to the tail, wraps around the lower edge, and closes back at the nose.

### `twist_fish_swim.dat`
This file defines a gentle **Twist Curve** for the fish demo.
- **Usage**: Load this as the "Twist curve" to add a small swimming-style turn instead of a dramatic helical twist.
- **Point layout**: Open polyline where `x` is height and `y` is twist angle in degrees. This version ramps slowly from `-5` to `10`.

## Quick Start

1. Open FoamCut and choose **Rotary / TwistRot**.
2. Click **Settings**.
3. In **Revolution Profile**, click **Load Polyline** and load `revolution_vase.dat`.
4. In **Rotation Curve**, click **Load Closed Polyline** and load `rotation_star.dat`.
5. In **Twist**, click **Load Twist Curve** and load `twist_linear.dat`.
6. Close Settings and inspect the 3D preview. You should see a twisted star-shaped vase.

## Reproduce The Fish Exactly

### Manual UI steps

1. Run the app with `npm run dev`.
2. Open `http://localhost:5173/?workflow=ROTARY`.
3. Click **Settings** in the top bar.
4. In **Revolution Profile**, scroll to **Custom profile tools** and click **Load Polyline**.
5. Choose `examples/twist_rot/revolution_chubby_fish.dat`.
6. Expected result:
   The left preview should show a fuller middle thickness profile, and the 3D preview should look like a soft ornament blank rather than a vase.
7. Expand **Rotation Curve**.
8. In **Cross-section tools**, click **Load Closed Polyline**.
9. Choose `examples/twist_rot/rotation_fish_body.dat`.
10. Expected result:
   The left watermark section should read as a fish outline with a rounded nose, body bulge, small fin bumps, and a forked tail.
11. Expand **Twist**.
12. In **Twist curve tools**, click **Load Twist Curve**.
13. Choose `examples/twist_rot/twist_fish_swim.dat`.
14. Expected result:
   The fish should keep its silhouette, but the body should pick up a light turning motion instead of a heavy corkscrew twist.
15. Press `Escape` to close Settings.
16. Click **TOP** in the 3D preview controls.
17. This is the most readable view for the fish. The fish will look less recognizable from strict side views because TwistRot is a rotary loft workflow.
18. Click **⚡ Generate Path**.
19. After generation, click **TOP** again and then **Table** to compare the fish outline with the rotary sweep path.
20. Use **File** → **Cut by Table** to export the table-style G-code.

### Automated demo steps

1. Regenerate the fish demo spec:
   `node demos/scripts/generate.mjs --file demos/demo-files/advanced-workflows-rotary-twistrot-chubby-fish.demo.txt`
2. Start the app:
   `npm run dev`
3. In another terminal, run the demo:
   `PW_SKIP_WEBSERVER=1 npx playwright test demos/generated/advanced-workflows-rotary-twistrot-chubby-fish.spec.ts`
4. The recording and step log will appear under `demos/results/advanced-workflows-rotary-twistrot-chubby-fish-demo-chromium-.../`.

### Files used by the fish demo

- `examples/twist_rot/revolution_chubby_fish.dat`
- `examples/twist_rot/rotation_fish_body.dat`
- `examples/twist_rot/twist_fish_swim.dat`
- `demos/demo-files/advanced-workflows-rotary-twistrot-chubby-fish.demo.txt`
