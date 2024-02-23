<template>
  <div ref="container"></div>
</template>

<script>
import * as THREE from "three";
import { TextGeometry } from 'three/addons/geometries/TextGeometry.js';

export default {
  mounted() {
    const renderer = new THREE.TextGeometry( text, parameters );
};
</script>
