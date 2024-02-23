<template>
  <div ref="container"></div>
</template>

<script>
import * as THREE from "three";
import { FontLoader } from "three/addons/loaders/FontLoader.js";
import { TextGeometry } from "three/addons/geometries/TextGeometry.js";

import { GUI } from "three/addons/libs/lil-gui.module.min.js";

export default {
  mounted() {
    // Cargar la fuente de tipografía
    const loader = new FontLoader();
    loader.load(
      "https://cdn.rawgit.com/mrdoob/three.js/master/examples/fonts/helvetiker_regular.typeface.json",
      function (font) {
        // Crea la escena
        const scene = new THREE.Scene();

        // Crea la cámara
        const camera = new THREE.PerspectiveCamera(
          50,
          window.innerWidth / window.innerHeight,
          0.1,
          200
        );
        camera.position.set(0, 0, 10);

        // Crea el renderizador
        const renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // Crea la geometría del texto
        const textGeometry = new TextGeometry("soccerjam chile", {
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

        // Centrar el texto
        textGeometry.computeBoundingBox();
        const textWidth = textGeometry.boundingBox.max.x - textGeometry.boundingBox.min.x;
        textGeometry.translate(-0.5 * textWidth, 0, 0);

        // Crea el material
        const textMaterial = new THREE.MeshBasicMaterial({ color: 0x00ff00 });

        // Crea la malla del texto
        const textMesh = new THREE.Mesh(textGeometry, textMaterial);

        // Añade la malla a la escena
        scene.add(textMesh);

        // Crea una luz
        const light = new THREE.PointLight(0xffffff, 1, 100);
        light.position.set(10, 10, 10);
        scene.add(light);

        // Añade una animación
        function animate() {
          requestAnimationFrame(animate);

          // Rotar el texto
          textMesh.rotation.y += 0.01;

          renderer.render(scene, camera);
        }

        animate();
      }
    );
  },
};
</script>

<style>
.info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}
</style>
