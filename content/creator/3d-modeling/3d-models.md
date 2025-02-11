---
date: 2018-01-09
title: 3D model essentials
description: Learn what assets and components are supported in external 3D models and how to configure them before importing them to Decentraland.
aliases:
  - /sdk-reference/external-3d-models/
  - /development-guide/external-3d-models/
  - /3d-modeling/3d-models/
categories:
  - 3d-modeling
type: Document
url: /creator/3d-modeling/3d-models
---

3D models are imported into decentraland in glTF format. There are a number of supported features that these models can include. This section goes over ways to make them compatible with Decentraland and best practices.

See [Set entity position]({{< ref "/content/creator/scenes/3d-essentials/entity-positioning.md" >}}) for information on how you can configure a 3D model in a Decentraland scene to set its position, scale, etc.

Keep in mind that all models, their shaders and their textures must be within the parameters of the [scene limitations]({{< ref "/content/creator/scenes/optimizing/scene-limitations.md" >}}).

## Supported 3D model formats

All 3D models in Decentraland must be in glTF format. [glTF](https://www.khronos.org/gltf) (GL Transmission Format) is an open project by Khronos providing a common, extensible format for 3D assets that is both efficient and highly interoperable with modern web technologies.

glTF models can have either a _.gltf_ or a _.glb_ extension. glTF files are human-readable, you can open one in a text editor and read it like a JSON file. This is useful, for example, to verify that animations are properly attached and to check for their names. glb files are binary, so they're not readable but they are considerably smaller in size, which is good for the scene's performance.

We recommend using _.gltf_ while you're working on a scene, but then switching to _.glb_ when uploading it.

The following aspects of a 3D model can either be embedded in a _glTF_ file or referenced externally:

- Textures can either be embedded or referenced from an external image file.
- Binary data about geometry, animations, and other buffer-related aspects of the model can either be embedded or referenced from an external _.bin_ file.

> Note: Animations _must_ be embedded inside the _glTF_ file to use in Decentraland.

#### Export to glTF from Blender

When exporting 3D models that include multiple animations, make sure that all animations are embedded in the model. To do this, open the _NLA editor_ and click _Stash_ to add each animation to the model.

We recommend using the following export settings when exporting models with animations:

<img src="/images/media/blender-export-settings-animations.png" alt="Blender export menu" width="250"/>

#### Export to glTF from 3D Studio Max

3D Studio Max doesn't support exporting to glTF by default, but you can install a plugin to enable it.

1. Download the plugin from [this link](https://github.com/BabylonJS/Exporters/tree/master/3ds%20Max).
2. Install the plugin by following [these instructions](http://doc.babylonjs.com/resources/3dsmax#how-to-install-the-3ds-max-plugin).
3. Export glTF files using the plugin by following [these instructions](http://doc.babylonjs.com/resources/3dsmax_to_gltf).

#### Export to glTF from Maya

Maya doesn't support exporting to glTF by default, but you can install a plugin to enable it.

1. Install the plugin by following [these instructions](http://doc.babylonjs.com/resources/maya).
2. Export glTF files using the plugin by following [these instructions](http://doc.babylonjs.com/resources/maya_to_gltf#pbr-materials).

> Note: As an alternative, you can try [this other plugin](https://github.com/WonderMediaProductions/Maya2glTF) too.

#### Export to glTF from Unity

Unity doesn't support exporting to glTF by default, but you can install a plugin to enable it.

Download the plugin from [this link](https://github.com/sketchfab/Unity-glTF-Exporter).

> Note: As an alternative, you can try [this other plugin](https://assetstore.unity.com/packages/tools/utilities/collada-exporter-for-unity2017-99793) too.

#### Export to glTF from SketchUp

SketchUp doesn't support exporting to glTF by default, but you can install a plugin to enable it.

Download the plugin from [this link](https://extensions.sketchup.com/en/content/gltf-exporter).

#### Preview a glTF model

A quick and easy way to preview the contents of a glTF model before importing it into a scene is to use the [Babylon.js Sandbox](https://sandbox.babylonjs.com/). Just drag and drop the glTF file (and its _.bin_ file if applicable) into the canvas to view the model.

In the sandbox you can also view the animations that are embedded in the model, select which to display by picking it out of a dropdown menu.

![](/images/media/babylon-sandbox.png)

#### Why we use glTF

Compared to the older _OBJ format_, which supports only vertices, normals, texture coordinates, and basic materials,
glTF provides a more powerful set of features that includes:

- Hierarchical objects
- Skeletal structure and animation
- More robust materials and shaders
- Scene information (light sources, cameras)

Compared to _COLLADA_, the supported features are very similar. However, because glTF focuses on providing a
"transmission format" rather than an editor format, it is more interoperable with web technologies.

Consider this analogy: the .PSD (Adobe Photoshop) format is helpful for editing 2D images, but images must then be converted to .JPG for use
on the web. In the same way, COLLADA may be used to edit a 3D asset, but glTF is a simpler way of transmitting it while rendering the same result.

## Convert fbx into glTF

_.fbx_ is a very popular standard for 3D models. It's not supported by our engine, but you can easily export an _.fbx_ model to _.gltf_ format.

We recommend using these tools:

- [Facebook's CLI tool](https://github.com/facebookincubator/FBX2glTF): this is the most robust alternative, but requires using the command line.

- [Blackthread](https://blackthread.io/gltf-converter): This the most complete web based tool. Less robust than the CLI, but a lot easier to use.

* [Modelconverter](https://modelconverter.com/convert.html): Another easy-to-use web based tool.

## Optimize a glTF

The following tool offers some optimizations that will make 3D models lighter and faster to download for players in your scene.

[glTF pipeline](https://github.com/AnalyticalGraphicsInc/gltf-pipeline)

Among other things, it converts _.gltf_ format into _.glb_, which is binary and so occupies a lot less. It also places texture files outside the 3D model, which allows you to use the same texture on multiple models.

> Note: _.glb_ format by default always has textures embedded in the file. The engine can't recognize two embedded textures as the same, they need to be external files that share a same hash.

## See also

The following pages also cover topics related to 3D models for Decentraland:

- [Materials]({{< ref "/content/creator/3d-modeling/materials.md" >}})
- [Meshes]({{< ref "/content/creator/3d-modeling/meshes.md" >}})
- [Colliders]({{< ref "/content/creator/3d-modeling/colliders.md" >}})
- [Animations]({{< ref "/content/creator/3d-modeling/animations.md" >}})
