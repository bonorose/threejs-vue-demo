<template>
    <canvas class="webgl" id="container"></canvas>
</template>

<script>
import * as THREE from 'three'
import * as dat from 'dat.gui'

let camera = null;
let scene = new THREE.Scene();
let renderer = new THREE.WebGLRenderer({antialias: true});
let mesh = null;

export default {
  name: 'Viewer3D',
  data() {
    return {
        loaded: false,
        // Loaders
        textureLoader: null,
        modelLoader: null,
        // GUI Debugger
        gui: new dat.GUI( {closeOnTop: true, closed:true} ),
        // Scene
        // camera: camera,
        // scene: scene,
        // renderer: renderer,
        // mesh: mesh,
    }
  },
  computed:{
  },
  methods: {
    init: function() {
        let container = document.getElementById('container');

        camera = new THREE.PerspectiveCamera(75, window.innerWidth, window.innerHeight, 0.01, 100);
        camera.position.z = 1;

        // scene = new THREE.Scene();

        let geometry = new THREE.BoxGeometry(20, 20, 20);
        let material = new THREE.MeshStandardMaterial( {color:0xffff00} );

        mesh = new THREE.Mesh(geometry, material);
        scene.add(mesh);

        // renderer = new THREE.WebGLRenderer({antialias: true});
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);
    },
    animate: function(){
        mesh.rotation.x += 0.01
        mesh.rotation.y += 0.02
        renderer.render(scene, camera)
        window.requestAnimationFrame(this.animate)
    },
  },
  mounted() {
      this.init()
      this.animate()
  },
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
