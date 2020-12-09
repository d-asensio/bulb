# 💡 Bulb

While working on side projects I often come with ideas about projects that could make my life easier if they would exist. This repo is my attempt for documenting such ideas.

<p align="center">
    <img src="./img/bulb_logo.png" alt="Pablo Picaso's Guernica painting, cropped and highlighting the bulb" />
</p>

> Inspiration exists, but it has to find us working.
> - Pablo Picasso

---

### GUI for quick prototyping using javascript proxies.

The idea is to make something like [dat.gui](https://github.com/dataarts/dat.gui) but using [proxies](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) to trigger updates when the objects change. Also it would be great to make it extensible and allow to create new controls.

#### Draft API

```java
// The entire ui is generated from an object
const uiDefinition = {
  camera: {
    type: 'folder',
    position3D: {
      type: 'coordinates',
      name: 'Position 3D',
      range: {
        x: [-1000, 1000],
        y: [0, 1000],
        z: [-500, 100]
      },
      step: 1,
      value: { x: -150, y: 280, z: 400 },
      updateFn: _updateCameraPosition
    },
    position2D: {
      type: 'coordinates',
      name: undefined,      // Name is deduced from the key if it is not defined
      range: [-1000, 1000], // Same range for all axis
      step: 1,
      value: { x: -150, y: 280, z: 400 },
      updateFn: _updateCameraPosition
    },
    zoom: {
      type: 'value',
      range: [0, 10],
      step: 0.01,
      value: 7,
      updateFn: _updateCameraZoom
    }
  },
}

const ui = new ProtoUI(uiDefinition)

// Retrieve the params object
const { camera } = ui.getParamsObject()

// Access to a property
const { x, y, z } = camera.position3D

// Modify a property directly (triggers an update)
camera.position3D.x += 30
```