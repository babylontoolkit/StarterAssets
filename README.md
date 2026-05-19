# Using Exported Unity Content

![Unity Starter Assets](./Screenshot.png)


## Babylon Toolkit Extension

A universal runtime library for advanced BabylonJS game development.

https://github.com/BabylonJS/BabylonToolkit


## Awesome Design Documents

https://github.com/voltagent/awesome-design-md


## Unity Asset Store

The Starter Assets are free and light-weight first and third person character base controllers for the latest Unity 2023 LTS Or Greater

https://assetstore.unity.com/packages/essentials/starter-assets-character-controllers-urp-267961


## Basic Installation
```bash
npm install babylonjs-toolkit
```

## Default Installation (UMD)
```bash
npm install babylonjs babylonjs-gui babylonjs-addons babylonjs-loaders babylonjs-materials babylonjs-inspector babylonjs-toolkit
```

* Global Import Side Effects (main.ts)
```javascript
import 'babylonjs';
import 'babylonjs-gui';
import 'babylonjs-loaders';
import 'babylonjs-materials';
import 'babylonjs-toolkit';
```

* TypeScript Configuration Settings (tsconfig.json)
```json
"types": [
    "babylonjs",
    "babylonjs-gui",
    "babylonjs-loaders",
    "babylonjs-gltf2interface",
    "babylonjs-materials",
    "babylonjs-toolkit"
]
```

Note: The **BABYLON** and **TOOLKIT** namespaces are globally accessible. Navigation is now bundled within the toolkit.
