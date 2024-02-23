<template>
  <div ref="container"></div>
</template>

<script>
import * as THREE from "three";
import { TextGeometry } from "three/addons/geometries/TextGeometry.js";

export default {
  mounted() {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);
    const loader = new FontLoader();

    loader.load("fonts/helvetiker_regular.typeface.json", function (font) {
      const geometry = new TextGeometry("Hello three.js!", {
        font: font,
        size: 80,
        height: 5,
        curveSegments: 12,
        bevelEnabled: true,
        bevelThickness: 10,
        bevelSize: 8,
        bevelOffset: 0,
        bevelSegments: 5,
      });
    });
  },
};
</script>
