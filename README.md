# Trinidad International Waterfront Centre — WebAR Prototype

This is a lightweight, no-build WebAR prototype.

## What it does
- Shows a simplified 3D architectural massing model of the Port of Spain International Waterfront Centre.
- Uses WebXR hit-testing to place the model on a detected horizontal surface on supported Android devices.
- Falls back to an interactive orbit/zoom 3D viewer when immersive AR is unavailable.
- Includes `qr.html` to generate the final QR code after deployment.

## Model scope
The model is intentionally a recognizable approximation, not a BIM model or survey-grade replica.
The proportions are based on publicly available descriptions of the complex:
- two ~26-storey office towers,
- a lower ~22-storey Hyatt hotel,
- a common waterfront/podium setting.

## Deploy
WebXR requires HTTPS.

Easy options:
1. GitHub Pages: upload these files to a repository and enable Pages.
2. Netlify Drop: deploy the folder as a static site.
3. Any government/enterprise HTTPS web server.

The public URL should point to `index.html`.

## Make the QR code
After deployment:
1. Open `qr.html`.
2. Paste the public HTTPS URL of the AR page.
3. Click **Generate QR**.
4. Save/print the displayed QR code.

## Phone testing
Best first test:
- Android phone
- Current Chrome
- ARCore-capable device
- Camera/AR permissions allowed

On unsupported devices, the page remains usable as a normal interactive 3D viewer.

## Production next steps
For a higher-fidelity version, replace the procedural massing model with a licensed `.glb/.gltf` model built from:
- architectural drawings/BIM,
- photogrammetry,
- LiDAR/scan data,
- or a commissioned Blender/Revit model.

You can also add labels, hotspots, videos, data overlays, audio narration, accessibility controls, or guided tours.


## Version 2 — clickable information hotspots

Two interactive hotspots have been added:

1. Ministry of Trade, Investment & Tourism — https://tradeind.gov.tt/
2. Global Trinidad and Tobago — https://globaltrinidadandtobago.com/

Interaction:
- Tap/click a white hotspot marker.
- An information card opens over the 3D/AR scene.
- Choose `Visit website` to open the linked site in a new tab.
- Choose `Continue exploring` to dismiss the card.

To add more hotspots, duplicate a `createHotspot({...})` block in `index.html` and update:
- `x`, `y`, `z` — 3D position
- `label` — short floating label
- `title` — panel heading
- `description` — panel copy
- `url` — destination link


## Welcome experience

Version 2 now opens with an investor-focused welcome screen:

> Welcome, Investor! Trinidad and Tobago is open for business!

The visitor selects **Explore the Waterfront** to enter the interactive 3D experience. From there they can:
- explore the model,
- tap the Ministry and GlobalTT information hotspots,
- or enter supported WebAR mode.

The welcome overlay is deliberately dismissed before requesting AR/camera access so the opening message remains readable and the visitor explicitly chooses to continue.


## GitHub Pages compatibility fix

This build adds an ES module import map for Three.js. The earlier build loaded
`OrbitControls.js` and `ARButton.js` directly, but those files import `three`
using a bare module specifier. Browsers cannot resolve that specifier unless an
import map or bundler is provided.

Use this `index.html` as the GitHub Pages version.

### Testing
1. Replace the repository's existing `index.html` with this fixed file.
2. Commit/push the change.
3. Open the GitHub Pages URL directly in the phone browser first.
4. Tap `Explore the Waterfront`.
5. Confirm the 3D model appears.
6. Then test the QR code.

### AR device note
The 3D viewer works broadly on modern browsers. Immersive WebXR AR is most
reliable on ARCore-capable Android devices using Chrome. iPhone/iPad Safari
does not provide the same WebXR immersive-AR path, so it may show the 3D
viewer without the full `Enter AR` experience.
