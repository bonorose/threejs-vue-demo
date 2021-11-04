<template>
  <div class='row'>
        <div class='col-lg-8'>
            <div class='container2 container' id="location">
                <h1>Three.js Models interactive demo</h1>
            </div>
        </div>

        <div class='col-lg-4'>
            <div class='col container optionsMenu'>
                <div class='row-lg-12'>
                    <h1>Options</h1>
                    <select class="form-select form-select-lg mb-3" aria-label=".form-select-lg example">
                        <option selected>Select Model</option>
                        <option value="0">Drawer</option>
                        <option value="1">L-Shaped Kitchen</option>
                        <option value="2">Parallel Kitchen</option>
                        <option value="3">Italian Kitchen</option>
                    </select>
                </div>
                <hr>
                <div class='row-lg-12'>
                    <h1>Materials</h1>
                </div>
                <div class='row-lg-12'>
                    <h2>Wood</h2>
                    <div class="row">
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/ballroom_1.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/studio_1.png);">
                    </div>
                </div>
    
                <div class='row-lg-12'>
                    <h2>Metal</h2>
                    <div class="row">
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/ballroom_1.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/studio_1.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/studio_2.png);">
                        </div>
                    </div>
                </div>

                <hr>

                <div class='row-lg-12'>
                    <h1>Lighting</h1> 
                    <div class="row">
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/ballroom_1.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/studio_1.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/studio_2.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/studio_3.png);">
                        </div>
                        <div class="col-lg-3 itemOption"
                        style="background-image: url(lighting/hall_1.png);">
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
  </div>
</template>

<!-- <script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script> -->

<script>
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader'
// import { RGBELoader } from 'three/examples/jsm/loaders/RGBELoader.js';
// import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import * as dat from 'dat.gui'

// Loading
const textureLoader = new THREE.TextureLoader()
const modelLoader = new GLTFLoader()

// Debug
const gui = new dat.GUI( {closeOnTop: true, closed:true} )
// console.log(gui)

// Canvas
const canvas = document.querySelector('canvas.webgl')

// RGB Loader
// const rgbeloader = new RGBELoader()
// rgbeloader.setPath( 'lighting/' )
// rgbeloader.load( 'studio_1.hdr', function ( texture ) {
//         texture.mapping = THREE.EquirectangularReflectionMapping
//         // scene.background = texture
//         scene.environment = texture
// })

// Scene
const scene = new THREE.Scene()

// Material
const woodMat = new THREE.MeshStandardMaterial()
// woodMat.roughness = 0.1
textureLoader.load('models/furniture/textures/diff.jpg',

    // onLoad callback
    function ( texture ) {
        // in this example we create the material when the texture is loaded
        woodMat.map = texture
    },

    // onProgress callback currently not supported
    undefined,

    // onError callback
    function ( err ) {
      console.error( 'An error happened: ', err )
    }
)
textureLoader.load('models/furniture/textures/normal.jpg',

    // onLoad callback
    function ( texture ) {
        // in this example we create the material when the texture is loaded
        woodMat.normalMap = texture
    },

    // onProgress callback currently not supported
    undefined,

    // onError callback
    function ( err ) {
      console.error( 'An error happened: ', err )
    }
)
textureLoader.load('models/furniture/textures/rough.jpg',

    // onLoad callback
    function ( texture ) {
        // in this example we create the material when the texture is loaded
        woodMat.roughnessMap = texture
    },

    // onProgress callback currently not supported
    undefined,

    // onError callback
    function ( err ) {
      console.error( 'An error happened: ', err )
    }
)

const woodMatOptions = {
    color: 0x121212
}


const metalMat = new THREE.MeshStandardMaterial( {} )
metalMat.metalness = 1
metalMat.roughness = 0.1
// metalMat.envMap = scene.environment

const metalMatOptions = {
    roughness: 0.1,
    metalness: 0.1,
    color: 0x121212
}

// Load a glTF resource
modelLoader.load(
	// resource URL
	'models/furniture/drawer.gltf',
	// called when the resource is loaded
	function ( gltf ) {
        // gltf.scene.traverse( function ( child ) {
        //     if ( child.isMesh ) {
        //         child.geometry.center(); // center here
        //     }
        // });
        // gltf.scene.scale.set(0.003, 0.003, 0.003);
        gltf.scene.children[0].receiveShadow = true

        // const woodenMaterial = gltf.scene.children[0].children[0].material
        // const metalMaterial = gltf.scene.children[0].children[1].material

        gltf.scene.children[0].children[1].material = metalMat
        gltf.scene.children[0].children[0].material = woodMat

        gltf.scene.position.set(-1, -2, 0)
		scene.add( gltf.scene );

		gltf.animations; // Array<THREE.AnimationClip>
		gltf.scene; // THREE.Group
		gltf.scenes; // Array<THREE.Group>
		gltf.cameras; // Array<THREE.Camera>
		gltf.asset; // Object


	},
	// called while loading is progressing
	function ( xhr ) {

		console.log( ( xhr.loaded / xhr.total * 100 ) + '% loaded' );

	},
	// called when loading has errors
	function ( error ) {

		console.log( 'An error happened: ', error );

	}
);

/*
 * Model Controls
 */
console.log(scene)
const modelOptions = gui.addFolder("Material Parameters")
const woodOptions = modelOptions.addFolder("Wood")
woodOptions.addColor(woodMatOptions, 'color')
    .onChange(() => {
        scene.children[3].children[0].children[0].material.color.set(woodMatOptions.color)
    })


const metalOptions = modelOptions.addFolder("Metal")
metalOptions.addColor(metalMatOptions, 'color')
    .onChange(() => {
        scene.children[3].children[0].children[1].material.color.set(metalMatOptions.color)
    })
metalOptions.add(metalMatOptions, 'roughness').min(0).max(1).step(.001)
    .onChange(() => {
        scene.children[3].children[0].children[1].material.roughness = metalMatOptions.roughness
    })
metalOptions.add(metalMatOptions, 'metalness').min(0).max(1).step(.001)
    .onChange(() => {
        scene.children[3].children[0].children[1].material.metalness = metalMatOptions.metalness
    })


/**
 * Sizes
 */
const sizes = {
    width: window.innerWidth,
    height: window.innerHeight
}

window.addEventListener('resize', () =>
{
    // Update sizes
    sizes.width = window.innerWidth
    sizes.height = window.innerHeight

    // Update camera
    camera.aspect = sizes.width / sizes.height
    camera.updateProjectionMatrix()

    // Update renderer
    renderer.setSize(sizes.width, sizes.height)
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
})

/**
 * Camera
 */
// Base camera
const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height, 0.1, 100)
camera.position.x = 5
camera.position.y = 4
camera.position.z = 7
scene.add(camera)

// const cameraSettings = gui.addFolder('Camera')
// cameraSettings.add(camera.position, 'x').step(0.01)
// cameraSettings.add(camera.position, 'y').step(0.01)
// cameraSettings.add(camera.position, 'z').step(0.01)
// cameraSettings.add(camera.rotation, 'x').step(0.01)
// cameraSettings.add(camera.rotation, 'y').step(0.01)
// cameraSettings.add(camera.rotation, 'z').step(0.01)

// Controls
// const controls = new OrbitControls(camera, canvas)
// controls.enableDamping = true

// Lights
const ambient = new THREE.HemisphereLight(0xffffbb, 0x080820, 3);
scene.add(ambient);
ambient.position.set(0,-1,0)

const ambientLightSettings = {
    intensity: 7.54,
    skyColor: 0xffffbb,
    groundColor: 0x080820
}

const ambientLight = gui.addFolder("Ambient Light")
ambientLight.add(ambientLightSettings, 'intensity').min(0).max(15).step(0.01)
 .onChange(() => {
     ambient.intensity = ambientLightSettings.intensity
 })

const light = new THREE.DirectionalLight(0xFFFFFF, 1);
light.position.set( 1, 10, 6);
scene.add(light);

/**
 * Renderer
 */
const renderer = new THREE.WebGLRenderer({
    canvas: canvas,
    alpha: true
})
renderer.setSize(sizes.width, sizes.height)
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
renderer.toneMapping = THREE.ACESFilmicToneMapping
renderer.toneMappingExposure = 1
renderer.outputEncoding = THREE.sRGBEncoding

/**
 * Animate
 */

// document.addEventListener('mousemove', onDocumentMouseMove)

// let mouseX = 0
// let mouseY = 0

// let targetX = 0
// let targetY = 0

// let scale = 0
// let targetScale = 0

// const windowHalfX = window.innerWidth / 2;
// const windowHalfY = window.innerHeight / 2;

// function onDocumentMouseMove(event) {
//     // mouseX = (event.clientX - windowHalfX)
//     // mouseY = (event.clientY - windowHalfY)
// }

// const clock = new THREE.Clock()

const tick = () =>
{

    // targetX = mouseX * .001
    // targetY = mouseY * .001
    // targetScale = scale

    // const elapsedTime = clock.getElapsedTime()

    // Update objects
    // sphere.rotation.y = .5 * elapsedTime

    // sphere.rotation.y += .25 * (targetX - sphere.rotation.y)
    // sphere.rotation.x += .05 * (targetY - sphere.rotation.x)
    // sphere.position.z += -.05 * (targetY - sphere.rotation.x)

    // Update Orbital Controls
    // controls.update()

    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}

tick()
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
*
{
    margin: 0;
    padding: 0;
}

html,
body
{
    height: 100vh;
    font-family: 'Poppins';
    background: rgb(31, 31, 31);
}

body {
    overflow-x: hidden;
}

#gui {
    position: inherit;
    top:2px;
    left:2px;
}

.webgl
{
    position: absolute;
    top: 0;
    left: 0;
    outline: none;
    mix-blend-mode: exclusion;
}

.optionsMenu {
    background: rgb(24, 24, 24);
    height: 100vh;
}

.itemOption {
    transition: .05s ease-in-out;
    background: rgb(110, 110, 110);
    width: 60px;
    height: 60px;
    margin: 5px;
    color:white;
    font-size: 0.95rem;
}

.itemOption:hover {
    transition: .05s ease-in-out;
    width: 65px;
    height: 65px;
    margin: 5px;
    background: rgb(165, 165, 165);
}

.container2 {
    height: 100vh;
    display: grid;
    place-items: top;
}

.textUnderlay {
    color: whitesmoke;
    background-color: rgba(255, 255, 255, 0.11);
    border-radius: 2rem;
    height: 50vh;
}

h1 {
    user-select: none;
    font-size: 5rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    text-transform: uppercase;
    color: whitesmoke;
    opacity: 0.35;
    background-color: rgba(23, 26, 39, 0.103);
}

h2 {
    user-select: none;
    font-size: 3rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    text-transform: uppercase;
    color: whitesmoke;
    opacity: 0.35;
}
</style>
