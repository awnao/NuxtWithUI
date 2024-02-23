<template>
  <div>
    <div ref="container"></div>
    <button @click="changeColor">Cambiar color</button>
    <button @click="changeFont">Cambiar fuente</button>
    <button @click="changeWeight">Cambiar peso</button>
    <button @click="changeBevel">Cambiar bisel</button>
  </div>
</template>

<script>
import * as THREE from "three";
import { FontLoader } from "three/addons/loaders/FontLoader.js";
import { TextGeometry } from "three/addons/geometries/TextGeometry.js";

import { GUI } from "three/addons/libs/lil-gui.module.min.js";

export default {
  mounted() {
    this.init();
    this.animate();
  },
  methods: {
    init() {
      const container = this.$refs.container;

      // CAMERA
      const camera = new THREE.PerspectiveCamera(
        30,
        this.getWindowWidth() / this.getWindowHeight(),
        1,
        1500
      );
      camera.position.set(0, 400, 700);

      const cameraTarget = new THREE.Vector3(0, 150, 0);

      // SCENE
      const scene = new THREE.Scene();
      scene.background = new THREE.Color(0x000000);
      scene.fog = new THREE.Fog(0x000000, 250, 1400);

      // LIGHTS
      const dirLight = new THREE.DirectionalLight(0xffffff, 0.4);
      dirLight.position.set(0, 0, 1).normalize();
      scene.add(dirLight);

      const pointLight = new THREE.PointLight(0xffffff, 4.5, 0, 0);
      pointLight.color.setHSL(Math.random(), 1, 0.5);
      pointLight.position.set(0, 100, 90);
      scene.add(pointLight);

      const materials = [
        new THREE.MeshPhongMaterial({ color: 0xffffff, flatShading: true }), // front
        new THREE.MeshPhongMaterial({ color: 0xffffff }), // side
      ];

      const group = new THREE.Group();
      group.position.y = 100;
      scene.add(group);

      const plane = new THREE.Mesh(
        new THREE.PlaneGeometry(10000, 10000),
        new THREE.MeshBasicMaterial({ color: 0xffffff, opacity: 0.5, transparent: true })
      );
      plane.position.y = 100;
      plane.rotation.x = -Math.PI / 2;
      scene.add(plane);

      // RENDERER
      const renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setPixelRatio(window.devicePixelRatio);
      renderer.setSize(this.getWindowWidth(), this.getWindowHeight());
      container.appendChild(renderer.domElement);

      // EVENTS
      container.style.touchAction = "none";

      window.addEventListener(
        "resize",
        () => this.onWindowResize(renderer, camera),
        false
      );

      // Gui
      const params = {
        changeColor: () => {
          pointLight.color.setHSL(Math.random(), 1, 0.5);
        },
        changeFont: () => {
          this.fontIndex++;
          this.fontName = this.reverseFontMap[
            this.fontIndex % this.reverseFontMap.length
          ];
          this.loadFont();
        },
        changeWeight: () => {
          this.fontWeight = this.fontWeight === "bold" ? "regular" : "bold";
          this.loadFont();
        },
        changeBevel: () => {
          this.bevelEnabled = !this.bevelEnabled;
          this.refreshText();
        },
      };

      const gui = new GUI();
      gui.add(params, "changeColor").name("Cambiar color");
      gui.add(params, "changeFont").name("Cambiar fuente");
      gui.add(params, "changeWeight").name("Cambiar peso");
      gui.add(params, "changeBevel").name("Cambiar bisel");
      gui.open();

      this.container = container;
      this.camera = camera;
      this.cameraTarget = cameraTarget;
      this.scene = scene;
      this.renderer = renderer;
      this.group = group;
      this.materials = materials;

      this.loadFont();
    },
    onWindowResize(renderer, camera) {
      camera.aspect = this.getWindowWidth() / this.getWindowHeight();
      camera.updateProjectionMatrix();
      renderer.setSize(this.getWindowWidth(), this.getWindowHeight());
    },
    getWindowWidth() {
      return typeof window !== "undefined" ? window.innerWidth : 800; // Valor predeterminado si window no está disponible
    },
    getWindowHeight() {
      return typeof window !== "undefined" ? window.innerHeight : 600; // Valor predeterminado si window no está disponible
    },
    loadFont() {
      const loader = new FontLoader();
      loader.load(
        "https://cdn.rawgit.com/mrdoob/three.js/master/examples/fonts/" +
          this.fontName +
          "_" +
          this.fontWeight +
          ".typeface.json",
        (response) => {
          this.font = response;
          this.refreshText();
        }
      );
    },
    createText() {
      this.textGeo = new TextGeometry(this.text, {
        font: this.font,
        size: this.size,
        height: this.height,
        curveSegments: this.curveSegments,
        bevelThickness: this.bevelThickness,
        bevelSize: this.bevelSize,
        bevelEnabled: this.bevelEnabled,
      });

      this.textGeo.computeBoundingBox();

      const centerOffset =
        -0.5 * (this.textGeo.boundingBox.max.x - this.textGeo.boundingBox.min.x);

      this.textMesh1 = new THREE.Mesh(this.textGeo, this.materials);

      this.textMesh1.position.x = centerOffset;
      this.textMesh1.position.y = this.hover;
      this.textMesh1.position.z = 0;

      this.textMesh1.rotation.x = 0;
      this.textMesh1.rotation.y = Math.PI * 2;

      this.group.add(this.textMesh1);

      if (this.mirror) {
        this.textMesh2 = new THREE.Mesh(this.textGeo, this.materials);

        this.textMesh2.position.x = centerOffset;
        this.textMesh2.position.y = -this.hover;
        this.textMesh2.position.z = this.height;

        this.textMesh2.rotation.x = Math.PI;
        this.textMesh2.rotation.y = Math.PI * 2;

        this.group.add(this.textMesh2);
      }
    },
    refreshText() {
      this.group.remove(this.textMesh1);
      if (this.mirror) this.group.remove(this.textMesh2);

      if (!this.text) return;

      this.createText();
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.render();
    },
    render() {
      this.group.rotation.y += (this.targetRotation - this.group.rotation.y) * 0.05;

      this.camera.lookAt(this.cameraTarget);

      this.renderer.render(this.scene, this.camera);
    },
  },
  data() {
    return {
      container: null,
      camera: null,
      cameraTarget: null,
      scene: null,
      renderer: null,
      group: null,
      textMesh1: null,
      textMesh2: null,
      textGeo: null,
      materials: null,
      firstLetter: true,
      text: "three.js",
      bevelEnabled: true,
      font: undefined,
      fontName: "optimer", // helvetiker, optimer, gentilis, droid sans, droid serif
      fontWeight: "bold", // normal bold
      height: 20,
      size: 70,
      hover: 30,
      curveSegments: 4,
      bevelThickness: 2,
      bevelSize: 1.5,
      mirror: true,
      fontIndex: 1,
      reverseFontMap: [
        "helvetiker",
        "optimer",
        "gentilis",
        "droid/droid_sans",
        "droid/droid_serif",
      ],
      reverseWeightMap: ["regular", "bold"],
      targetRotation: 0,
      targetRotationOnPointerDown: 0,
      pointerX: 0,
      pointerXOnPointerDown: 0,
      windowHalfX: this.getWindowWidth() / 2,
    };
  },
};
</script>
