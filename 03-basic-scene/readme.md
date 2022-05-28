# 03. Basic Scene

Three.js makes the work the simplest possible way

Basic Scene can be created with No bundler, no modules, no dependencies

A JavaScript and a HTML file

---

- Go to http://threejs.org/

- Click on the Download

- UnZip

- Go to the build/folder

- copy the three.min.js file to your project

---

## How to use Three.js

- We have access to variable **THREE**
- It contains most of the classes and properties but not all of them
- Always use uppercase
- Log it in the console with console.log(THREE)

---

## 4 Elements to get Started

1. Scene
2. Objects
3. Camera
4. Renderer

---

## Scene

It is like a Container

We put objects, models, lights etc. in it

At some point we ask. Three.js to render that scene

---

## Objects

It can be many things like primitive geometries, Imported models, particles, lights etc.

We Start with a simple red cube

To create a Visible object

- We need to create a **Mesh**
- Combination of a geometry (the shape) and a material (how it looks)
- Start with a **Box Geometry** and a **Mesh Basic Material**

### Geometry

Instantiate a **BoxGeometry**

```javascript
const geometry = new THREE.BoxGeometry(1, 1, 1)
```

The first 3 parameters corresponds to the box's size.

### Material

Instantiate a **MeshBasicMaterial**

```javascript
const material = new THREE.MeshBasicMaterial({ color: '#ff0000' })
```

There are Multiple ways to express a color

​		0xff000

​		'#ff000'

​		'red'

### Mesh

Instantiate the **Mesh** with the geometry and the material

```javascript
const mesh = new THREE.Mesh(geometry, material)
```

Add it to the scene with add(...) method

```javascript
scene.add(mesh)
```

---

## Camera

- It will not Visible

- serve as point of view when doing a render

- Can have mutiple cameras and switch between them

- There are different types

```javascript
const camera = new THREE.PerspectiveCamera()
scene.add(camera)
```

### Field of View (fov)

- Vertical vision angle
- In degrees
- For this exercise we will use a 75 degree angle

```javascript
const camera = new THREE.PerspectiveCamera(75)
scene.add(camera)
```

### Aspect Ratio

- The width of the render divided by the height of the render
- we don't have a render yet, but we can decide on a size now.
- Create a sizes object containing temporary values

```javascript
const sizes = {
  width: 800,
  height: 600
}
const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height)
scene.add(camera)
```

---

## Renderer

- Render the scene from the camera point of view.
- Results are drawn into a canvas
- A canvas is a HTML element in which you can draw stuff
- Three.js will use WebGL to draw the render inside the canvas
- You can create it or you can let Three.js do it
- Create the <canvas> element before you load the scripts with a webgl class

```html
<canva class="webgl"></canvas>
```

- Create the WebGL renderer with an empty object

```javascript
const renderer = new THREE.WebGLRenderer({
  ...
})
```

- use document.querySelector(...) to retrieve the canvas. We created in the HTML and store it in a canvas variable

```javascript
const canvas = document.querySelector("canvas.webgl")
const renderer = new THREE.WebGLRenderer({
  canvas
})
```

use the setSize(...) method to update the size of the renderer

```javascript
renderer.setSize(sizes.width, sizes.height)
```

call the render(...) method on the renderer with scene and the camera as parameters

```javascript
renderer.render(scene, camera)
```

Here nothing is visible because the camera is inside the cube. We need to move the camera backward.

To transform an object, we can use the following properties.

- Position
- rotation
- Scale

The position property is also an object with X, Y and Z properties.

Three.js considers the forward/backward axis to be Z

Move the camera backward before doing the render

```
camera.position.Z = 3
```