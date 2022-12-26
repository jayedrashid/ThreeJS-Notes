# `ThreeJS: Notes`

Three.js is a JavaScript-based WebGL engine that can run GPU-powered games and other graphics-powered apps straight from the browser. The three. js library provides many features and APIs for drawing 3D scenes in your browser.

<p align="center">
 <img width="600px" src="https://miro.medium.com/max/724/0*oGyg1mbyXIHa3TIX.png" align="center" alt="ThreeJS Beginners Guide" />
 <h2 align="center">ThreeJS Beginners Guide</h2>
</p>

---

## ThreeJS

Three.js is a cross-browser JavaScript library and application programming interface used to create and display animated 3D computer graphics in a web browser using WebGL.

Three.js is a 3D JavaScript library that enables developers to create 3D
experiences for the web.
It works with WebGL, but you can make it work with SVG and CSS but those
two are quite limited.


---

## ThreeJS Topics

- Basics:
    * Creating a first scene
    * Adding objects
    * Choosing the right materials
    * Adding textures
    * Animating everything
    
- Intermediate:
    * Creating our own geometries
    * Adding lights and shadows
    * Interacting with 3D objects
    * Adding particles

- Advance:
    * Physics
    * Realistic renders
    * Writing custom shaders
    * Adding post-processing
    * Creating our own models with Blender

---

## Amazing Three JS Web:
- http://bruno-simon.com
- https://go.pioneer.com/cornrevolution
- https://richardmattka.com
- https://lusion.co
- https://www.oculus.com/medal-of-honor/
- http://letsplay.ouigo.com
- https://live.vanmoof.com/site
- https://zen.ly
- https://prior.co.jp/discover
- https://www.midwam.com
- https://heraclosgame.com
- https://chartogne-taillet.com
- http://codeology.braintreepayments.com
- https://avseoul.github.io/particleEqualizer/index.html
- http://www.cryptarismission.com/#!/training-room/4
- https://kuva.io/hair-simulation/
- http://www.bjork.com/
- http://tympanus.net/codrops/2016/04/26/the-aviator-animating-basic-3d-scene-threejs/
- http://www.dennis.video/
- http://unseen-music.com/yume/
- http://www.onformative.com/work/porsche-blackbox
- http://audiograph.xyz/


---

## What is WebGL
- JavaScript API
- Renders triangles at a remarkable speed
- Result can be drawn in a <canvas>
- Compatible with most modern browsers
- Uses the Graphic Processing Unit (GPU)

WebGL is a JavaScript API for rendering interactive 2D and 3D graphics within any compatible web browser without the use of plug-ins. WebGL is fully integrated with other web standards, allowing GPU-accelerated usage of physics and image processing and effects as part of the web page canvas.

The CPU can do calculations really fast but one by one. The GPU is a little slower but can do thousands of parallel calculations. To draw a 3D model, the idea is to draw many triangles at the right position and colorize them so that they look the way we want. The GPU will position all those points at once according to many factors. Once the points are placed, the GPU will draw each visible pixel of those triangles. Again, those thousands of pixels will be calculated and drawn in parallel extremely fast.

The instructions to place the points and draw the pixels are written in shaders. We provide a bunch of information to those shaders like the points positions, model transformations, the camera coordinates and things get positions and colorize the way we want. This is why native WebGL is so hard. Drawing a single triangle on the canvas would take at least 100 lines of code. Native WebGL benefits from existing at a low level which enables optimizations and more control. Three.js drastically simplifythe process of all of this. We can still interact with the WebGL and we can create our own shader and provide our own information. 

Three.js is the most popular WebGL library, it's very stable, it provides many
features, the documentation is remarkable, the community is working hard on updates, and it's still close enough to native WebGL. But there are many other great libraries. Be curious, try them out.


---

## Getting Started

4 elements to get started:
  1. A scene that will contain objects
  2. Some objects
  3. A camera
  4. A renderer


SCENE
- Like a container
- We put objects, models, lights, etc. in it
- At some point we ask Three.js to render that scene:

```sh
const scene = new THREE.Scene ();
```

OBJECTS
- Primitive geometries
- Imported models
- Particles
- Lights


MESH
- We need to create a Mesh
- Combination of a geometry (the shape) and a material (how it looks).
- Start with a BoxGeometry and a MeshBasicMaterial.

GEOMETRY
- Instantiate a BoxGeometry
const geometry = new THREE.BoxGeometry(1, 1, 1);
The first 3 parameters correspond to the box's size.

MATERIAL
- Instantiate a MeshBasicMaterial

```sh
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
```

Multiple ways to express a color:
  * 0xff0000
  * ‘#ff0000’
  * ‘red'
  * Color

CAMERA
- Not visible
- Serve as point of view when doing a render
- Can have multiple and switch between them
- Different types
- We are going to dse PerspectiveCamera

```sh
cost camera = new THREE.PerspectiveCamera(...);
scene.add(camera);
```

Two essential CAMERA parameters:

1. THE FIELD OF VIEW
    * Vertical vision angle (video-1.mp4)
    * In degrees
    * Also called fov
For this exercise we will use a 75 degrees angle.

```sh
cost camera = new THREE.PerspectiveCamera(75,…);
scene.add(camera);
```

2. THE ASPECT RATIO
The width of the render divided by the height of the render. We don't have a render yet, but we can decide on a size now.
Create a sizes object containing temporary values.

```sh
// Sizes
const sizes = {
width: 800,
height: 600
}

// Camera
const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height);
scene.add(camera);
```

RENDERER
- Render the scene from the camera point of view
- Result drawn into a canvas
- A canvas is a HTML element in which you can draw stuff
- Three.js will use WebGL to draw the render inside this canvas
- You can create it or you can let Three.js do it


CANVAS
Create the <canvas> element before you load the scripts with a webgl class

```sh
<canvas class="webgl"></canvas>
```


---

## Bundler (Webpack)

Limitations of Using Library Script
- Loading Three.js with a <script> has limitations
- Doesn't include some of the classes
- We need those classes
- We need to run a server to emulate a website and for security reasons

That’s why we’re going to use:

Bundler
- A tool in which you send JavaScript, CSS, HTML, images, TypeScript, Stylus, Sass, etc.
- The bundler apply potential modifications and output a web-friendly "bundle".
- Can do more like local server, manage dependencies, improve compatibility, add modules support, optimize files, deploy, etc.


Webpack
- Most popular
- Handle most of our needs
- Good documentation
- Good community
- Well maintained
- Hard to configure

Webpack is a free and open-source module bundler for JavaScript. It is made primarily for JavaScript, but it can transform front-end assets such as HTML, CSS, and images if the corresponding loaders are included. Webpack takes modules with dependencies and generates static assets representing those modules.

Install npm to run dependencies

---

## TRANSFORM OBJECTS

There are 4 properties to transform objects:
- position
- scale
- rotation
- quaternion

All classes that inherit from the Object3D possess those properties like
PerspectiveCamera or Mesh.
You can see inheritance on top of the Three.js documentation.

Those properties will be compiled in matrices. 

MOVE OBJECTS
With position which has 3 properties:
  * ×
  * y
  * z

The direction of each axis is arbitrary. In Three.js, we consider:
  * y axis is going upward
  * z axis is going backward
  * × axis is going to the right

The distance of 1 unit is arbitrary too. You should think of 1 according to what you are building (1 centimeter, 1 meter, 1 kilometer). Play around with the position of the mesh and try to guess where the cube
will get. Do that before the render(...).

```sh
mesh.position.x = 0.7
mesh.position.y = - 0.6
mesh.position.z = 1
```

position inherit from Vector3 which has many useful methods. You can get the length of a vector. 
```sh
console.log(mesh.position.length());
```
It’s the distance between the center of the scene and our object’s position.



You can get the distance from another Vector3.
```sh
console.log(mesh.position.distanceTo(camera.position));
```
It’s the distance between the camera and the object.


You can normalize its values.
```sh
console.log(mesh.position.normalize());
```
It will reduce the vector length to 1.


You can change all 3 values of ×, y and z at once by using the set(…) method. 
mesh.position.set(0.7, - 0.6, 1);

---

## TRANSFORM OBJECTS



---
