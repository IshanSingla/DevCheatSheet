
************************************
# THREE.JS BASICS
************************************

### Basic Summary
```python
Scene(Like Container)                             Scenes allow you to set up what and where is to be rendered by three.js. This is where you place objects, lights and cameras. 
Objects                                           Can be many things(Geometries,Imported Model,Particles,Light Etc.)
Camera                                            Serve as a Point of View when doing a RENDER
Renderer                                          Renderer displays your beautifully crafted scenes using WEBGL
Webpack                                           The webpack is a type of application that is used for compiling JavaScript modules
```

### SCENE
```python
Creating the scene                                To actually be able to display anything with three.js, we need three things: scene, camera and renderer, so that we can render the scene with camera.
Geometry                                          Basic Shape/Size of Object that we are creating
Material(Complex)                                 Basic look of the object(Colors,Light-sensitivity Etc)
Mesh                                              A Mesh object in three.js is used to create an object with a buffer geometry, and a material
Animate                                           JavaScript Function used to animate the object created by position,rotation or scale.
//Basic Code

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>My first three.js app</title>
		<style>
			body { margin: 0; }
		</style>
	</head>
	<body>
		<script src="js/three.js"></script>
		<script>
			const scene = new THREE.Scene();
			const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

			const renderer = new THREE.WebGLRenderer();
			renderer.setSize( window.innerWidth, window.innerHeight );
			document.body.appendChild( renderer.domElement );

			const geometry = new THREE.BoxGeometry( 1, 1, 1 );
			const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
			const cube = new THREE.Mesh( geometry, material );
			scene.add( cube );

			camera.position.z = 5;

			function animate() {
				requestAnimationFrame( animate );

				cube.rotation.x += 0.01;
				cube.rotation.y += 0.01;

				renderer.render( scene, camera );
			};

			animate();
		</script>
	</body>
</html>
```

### Geometry 
```python
const geometry = new THREE.BufferGeometry();                                           A representation of mesh, line, or point geometry. Includes vertex positions, face indices, normals, colors, UVs, and custom attributes within buffers, reducing the cost of passing all this data to the GPU.
const geometry = new THREE.BoxGeometry( 1, 1, 1 );                                     BoxGeometry is a geometry class for a rectangular cuboid with a given 'width', 'height', and 'depth'
const geometry = new THREE.CapsuleGeometry( 1, 1, 4, 8 );                              CapsuleGeometry is a geometry class for a capsule with given radii and height. It is constructed using a lathe(Smooth Curves)
const geometry = new THREE.CircleGeometry( 5, 32 );                                    CircleGeometry is a simple shape of Euclidean geometry. It is constructed from a number of triangular segments that are oriented around a central point and extend as far out as a given radius
const geometry = new THREE.ConeGeometry( 5, 20, 32 );                                  A class for generating cone geometries
const geometry = new THREE.CylinderGeometry( 5, 5, 20, 32 );                           A class for generating cylinder geometries
const edges = new THREE.EdgesGeometry( geometry );                                     This can be used as a helper object to view the edges of a geometry
const geometry = new THREE.ExtrudeGeometry( shape, extrudeSettings );                  Creates extruded geometry from a path shape
const geometry = new THREE.LatheGeometry( points );                                    Creates meshes with axial symmetry like vases. The lathe rotates around the Y axis.
const geometry = new THREE.PlaneGeometry( 1, 1 );                                      A class for generating plane geometries
const geometry = new THREE.PolyhedronGeometry( verticesOfCube, indicesOfFaces, 6, 2 ); A polyhedron is a solid in three dimensions with flat faces. This class will take an array of vertices, project them onto a sphere, and then divide them up to the desired level of detail
const geometry = new THREE.RingGeometry( 1, 5, 32 );                                   A class for generating a two-dimensional ring geometry
const geometry = new THREE.SphereGeometry( 15, 32, 16 );                               A class for generating sphere geometries
const geometry = new THREE.TorusGeometry( 10, 3, 16, 100 );                            A class for generating torus geometries
const geometry = new THREE.TorusKnotGeometry( 10, 3, 100, 16 );                        Creates a torus knot, the particular shape of which is defined by a pair of coprime integers, p and q. If p and q are not coprime, the result will be a torus link
//TextGeometry                                                                         A class for generating text as a single geometry. It is constructed by providing a string of text, and a set of parameters consisting of a loaded font and settings for the geometry's parent ExtrudeGeometry.

const loader = new FontLoader();

loader.load( 'fonts/helvetiker_regular.typeface.json', function ( font ) {

const geometry = new TextGeometry( 'Hello three.js!', {
		font: font,
		size: 80,
		height: 5,
		curveSegments: 12,
		bevelEnabled: true,
		bevelThickness: 10,
		bevelSize: 8,
		bevelOffset: 0,
		bevelSegments: 5
	} );
} );


```

### Material 
```python
const material = new THREE.MeshBasicMaterial();                                 A material for drawing geometries in a simple shaded (flat or wireframe) way.
const material = new THREE.MeshDepthMaterial();                                 A material for drawing geometry by depth. Depth is based off of the camera near and far plane. White is nearest, black is farthest.Alternative way to make the text contained in the tag as italic 
const material = new THREE.MeshDistanceMaterial();                              MeshDistanceMaterial is internally used for implementing shadow mapping with PointLights
const material = new THREE.MeshLambertMaterial();                               A material for non-shiny surfaces, without specular highlights.
const material = new THREE.MeshMatcapMaterial();                                MeshMatcapMaterial is defined by a MatCap (or Lit Sphere) texture, which encodes the material color and shading
const material = new THREE.MeshNormalMaterial();                                A material that maps the normal vectors to RGB colors 
const material = new THREE.MeshPhongMaterial();                                 A material for shiny surfaces with specular highlights
const material = new THREE.MeshStandardMaterial();                              A standard physically based material, using Metallic-Roughness workflow
const material = new THREE.MeshToonMaterial();                                  A material implementing toon shading
const material = new THREE.PointsMaterial();                                    The default material used by Points.
const material = new THREE.RawShaderMaterial();                                 This class works just like ShaderMaterial, except that definitions of built-in uniforms and attributes are not automatically prepended to the GLSL shader code
const material = new THREE.ShaderMaterial();                                    A material rendered with custom shaders. A shader is a small program written in GLSL that runs on the GPU
```

### Mesh 
```python
const mesh = new THREE.Mesh( geometry, material );                               Class representing triangular polygon mesh based objects. Also serves as a base for other classes such as SkinnedMesh
```

### Texture 
```python
//CubeTextureLoader
const scene = new THREE.Scene();
scene.background = new THREE.CubeTextureLoader()
	.setPath( 'textures/cubeMaps/' )
	.load( [
		'px.png',
		'nx.png',
		'py.png',
		'ny.png',
		'pz.png',
		'nz.png'
	] );                                                                                       Class for loading a CubeTexture. This uses the ImageLoader internally for loading files

//TextureLoader
const texture = new THREE.TextureLoader().load( 'textures/land_ocean_ice_cloud_2048.jpg' );        Class for loading a texture. This uses the ImageLoader internally for loading files.
 
```


### Lights 
```python
const light = new THREE.AmbientLight( 0x404040 );                                     This light globally illuminates all objects in the scene equally.This light cannot be used to cast shadows as it does not have a direction
const directionalLight = new THREE.DirectionalLight( 0xffffff, 0.5 );                 A light that gets emitted in a specific direction. This light will behave as though it is infinitely far away and the rays produced from it are all parallel
const light = new THREE.HemisphereLight( 0xffffbb, 0x080820, 1 );                     A light source positioned directly above the scene, with color fading from the sky color to the ground color
const light = new THREE.PointLight( 0xff0000, 1, 100 );                               A light that gets emitted from a single point in all directions. A common use case for this is to replicate the light emitted from a bare lightbulb
const rectLight = new THREE.RectAreaLight( 0xffffff, intensity,  width, height );     RectAreaLight emits light uniformly across the face a rectangular plane. This light type can be used to simulate light sources such as bright windows or strip lighting
const spotLight = new THREE.SpotLight( 0xffffff );                                    This light gets emitted from a single point in one direction, along a cone that increases in size the further from the light it gets

```



### Particles 
```python
//Basic Code For Particles Generation

const vertices = [];

for ( let i = 0; i < 10000; i ++ ) {

	const x = THREE.MathUtils.randFloatSpread( 2000 );
	const y = THREE.MathUtils.randFloatSpread( 2000 );
	const z = THREE.MathUtils.randFloatSpread( 2000 );

	vertices.push( x, y, z );

}

const geometry = new THREE.BufferGeometry();
geometry.setAttribute( 'position', new THREE.Float32BufferAttribute( vertices, 3 ) );

const material = new THREE.PointsMaterial( { color: 0x888888 } );

const points = new THREE.Points( geometry, material );

scene.add( points );

```

### RayCaster 
```python
//Raycaster                                          This class is designed to assist with raycasting. Raycasting is used for mouse picking (working out what objects in the 3d space the mouse is over) amongst other things.

const raycaster = new THREE.Raycaster();
const pointer = new THREE.Vector2();

function onPointerMove( event ) {

	// calculate pointer position in normalized device coordinates
	// (-1 to +1) for both components

	pointer.x = ( event.clientX / window.innerWidth ) * 2 - 1;
	pointer.y = - ( event.clientY / window.innerHeight ) * 2 + 1;

}

function render() {

	// update the picking ray with the camera and pointer position
	raycaster.setFromCamera( pointer, camera );

	// calculate objects intersecting the picking ray
	const intersects = raycaster.intersectObjects( scene.children );

	for ( let i = 0; i < intersects.length; i ++ ) {

		intersects[ i ].object.material.color.set( 0xff0000 );

	}

	renderer.render( scene, camera );

}

window.addEventListener( 'pointermove', onPointerMove );

window.requestAnimationFrame(render);
```


### Import Models 
```python
//Loading 3D models                              3D models are available in hundreds of file formats, each with different purposes, assorted features, and varying complexity which can be used in Frontend integration to beautify it.

//Loading                                        Only a few loaders (e.g. ObjectLoader) are included by default with three.js — others should be added to your app individually.

//Basic Code 

import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
const loader = new GLTFLoader();

loader.load( 'path/to/model.glb', function ( gltf ) {

	scene.add( gltf.scene );

}, undefined, function ( error ) {

	console.error( error );

} );
```


Made By - Yakshit
