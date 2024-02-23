<template>
  <div ref="container"></div>
</template>

<script>
import * as THREE from "three";

export default {
  mounted() {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );
    camera.position.z = 5;

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    this.$refs.container.appendChild(renderer.domElement);

    const loader = new THREE.FontLoader();
    loader.load(
      "https://cdn.rawgit.com/mrdoob/three.js/master/examples/fonts/helvetiker_regular.typeface.json",
      function (font) {
        const textGeometry = new THREE.TextGeometry("Texto 3D", {
          font: font,
          size: 1,
          height: 0.5,
          curveSegments: 12,
          bevelEnabled: true,
          bevelThickness: 0.03,
          bevelSize: 0.02,
          bevelOffset: 0,
          bevelSegments: 5,
        });
        const textMaterial = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
        const textMesh = new THREE.Mesh(textGeometry, textMaterial);
        scene.add(textMesh);
      }
    );

    const light = new THREE.PointLight(0xffffff, 1, 100);
    light.position.set(10, 10, 10);
    scene.add(light);

    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera);
    }
    animate();
  },
};
</script>
