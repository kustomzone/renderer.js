renderer.js
-----------

Renderer.js is a lightweight & flexible 3D scene graph library for web apps and games.
It uses the library [litegl.js](https://github.com/jagenjo/litegl.js) as a low level layer for WebGL.
It provides common useful classes such as;

* Scene and SceneNode
* Camera
* Renderer
* SkeletalAnimation
* ParticleEmissor

(incl. liteGL's Mesh, Shader and Texture)

Demo
-----

Check the examples folder to see the examples, or visit [this website](http://tamats.com/projects/rendeer/examples).
There's a boilerplate template to create an application in the folder boilerlate/

Examples
--------

First include the library and dependencies

```html
<script src="js/gl-matrix-min.js"></script>
<script src="js/litegl.js"></script>
<script src="js/rendeer.js"></script>
```

Create the scene

```js
var scene = new RD.Scene();
```

Create the renderer

```js
var context = GL.create({width: window.innerWidth, height:window.innerHeight});
var renderer = new RD.Renderer(context);
```

Attach to DOM

```js
document.body.appendChild(renderer.canvas);
```

Get user input

```js
gl.captureMouse();
renderer.context.onmousedown = function(e) { ... }
renderer.context.onmousemove = function(e) { ... }

gl.captureKeys();
renderer.context.onkey = function(e) { ... }
```

Set camera

```js
var camera = new RD.Camera();
camera.perspective( 45, gl.canvas.width / gl.canvas.height, 1, 1000 );
camera.lookAt( [100,100,100],[0,0,0],[0,1,0] );
```

Create and register mesh

```js
var mesh = GL.Mesh.fromURL("data/mesh.obj");
renderer.meshes["mymesh"] = mesh;
```

load and register texture

```js
var texture = GL.Texture.fromURL("mytexture.png", { minFilter: gl.LINEAR_MIPMAP_LINEAR, magFilter: gl.LINEAR });
renderer.textures["mytexture.png"] = texture;
```

Compile and register shader

```js
var shader = new GL.Shader(vs_code, fs_code);
renderer.shaders["phong"] = shader;
```

Add a node to the scene

```js
var node = new RD.SceneNode();
node.color = [1,0,0,1];
node.mesh = "mymesh";
node.texture = "mytexture.png";
node.shader = "phong";
node.position = [0,0,0];
node.scale([10,10,10]);
scene.root.addChild(node);
```

Create main loop

```js
requestAnimationFrame(animate);
function animate() {
	requestAnimationFrame( animate );

	last = now;
	now = getTime();
	var dt = (now - last) * 0.001;
	renderer.render(scene, camera);
	scene.update(dt);
}
```

Utils
-----

Includes several commands in the utils folder to generate docs, check errors, or build a minified version.

Documentation
-------------

See docs folder, or check the docs on [glMatrix](http://glmatrix.com) for further info.
More details in the [starter guide](https://github.com/jagenjo/rendeer.js/blob/master/guides/README.md) folder.

Cloned from [jagenjo](https://github.com/jagenjo)
