<template>
  <div ref="container"></div>
</template>

<script>
import * as THREE from "three";
import { FontLoader } from "three/examples/jsm/loaders/FontLoader.js";
import { TextGeometry } from "three/examples/jsm/geometries/TextGeometry.js";

export default {
  mounted() {
    this.init();
    this.animate();
  },
  methods: {
    init() {
      this.container = this.$refs.container;

      // CAMERA
      this.camera = new THREE.PerspectiveCamera(
        30,
        window.innerWidth / window.innerHeight,
        1,
        1500
      );
      this.camera.position.set(0, 400, 700);
      this.cameraTarget = new THREE.Vector3(0, 150, 0);

      // SCENE
      this.scene = new THREE.Scene();
      this.scene.background = new THREE.Color(0x000000);
      this.scene.fog = new THREE.Fog(0x000000, 250, 1400);

      // LIGHTS
      const dirLight = new THREE.DirectionalLight(0xffffff, 0.4);
      dirLight.position.set(0, 0, 1).normalize();
      this.scene.add(dirLight);

      const pointLight = new THREE.PointLight(0xffffff, 4.5, 0, 0);
      pointLight.color.setHSL(Math.random(), 1, 0.5);
      pointLight.position.set(0, 100, 90);
      this.scene.add(pointLight);

      this.materials = [
        new THREE.MeshPhongMaterial({ color: 0xffffff, flatShading: true }), // front
        new THREE.MeshPhongMaterial({ color: 0xffffff }), // side
      ];

      this.group = new THREE.Group();
      this.group.position.y = 100;
      this.scene.add(this.group);

      const plane = new THREE.Mesh(
        new THREE.PlaneGeometry(10000, 10000),
        new THREE.MeshBasicMaterial({ color: 0xffffff, opacity: 0.5, transparent: true })
      );
      plane.position.y = 100;
      plane.rotation.x = -Math.PI / 2;
      this.scene.add(plane);

      // RENDERER
      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.container.appendChild(this.renderer.domElement);

      // EVENTS
      this.container.style.touchAction = "none";
      this.container.addEventListener("pointerdown", this.onPointerDown);

      window.addEventListener("resize", this.onWindowResize);

      // Font loading
      this.loadFont();
    },
    onWindowResize() {
      this.windowHalfX = window.innerWidth / 2;

      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();

      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },
    loadFont() {
      const loader = new FontLoader();
      loader.load(
        "fonts/" + this.fontName + "_" + this.fontWeight + ".typeface.json",
        (response) => {
          this.font = response;
          this.refreshText();
        }
      );
    },
    createText() {
      if (!this.font) return;

      const textGeo = new TextGeometry(this.text, {
        font: this.font,
        size: this.size,
        height: this.height,
        curveSegments: this.curveSegments,
        bevelThickness: this.bevelThickness,
        bevelSize: this.bevelSize,
        bevelEnabled: this.bevelEnabled,
      });

      textGeo.computeBoundingBox();

      const centerOffset = -0.5 * (textGeo.boundingBox.max.x - textGeo.boundingBox.min.x);

      this.textMesh1 = new THREE.Mesh(textGeo, this.materials);

      this.textMesh1.position.x = centerOffset;
      this.textMesh1.position.y = this.hover;
      this.textMesh1.position.z = 0;

      this.textMesh1.rotation.x = 0;
      this.textMesh1.rotation.y = Math.PI * 2;

      this.group.add(this.textMesh1);

      if (this.mirror) {
        this.textMesh2 = new THREE.Mesh(textGeo, this.materials);

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
    onPointerDown(event) {
      if (event.isPrimary === false) return;

      this.pointerXOnPointerDown = event.clientX - this.windowHalfX;
      this.targetRotationOnPointerDown = this.targetRotation;

      document.addEventListener("pointermove", this.onPointerMove);
      document.addEventListener("pointerup", this.onPointerUp);
    },
    onPointerMove(event) {
      if (event.isPrimary === false) return;

      this.pointerX = event.clientX - this.windowHalfX;
      this.targetRotation =
        this.targetRotationOnPointerDown +
        (this.pointerX - this.pointerXOnPointerDown) * 0.02;
    },
    onPointerUp() {
      if (event.isPrimary === false) return;

      document.removeEventListener("pointermove", this.onPointerMove);
      document.removeEventListener("pointerup", this.onPointerUp);
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.render();
    },
    render() {
      this.group.rotation.y += (this.targetRotation - this.group.rotation.y) * 0.05;
      this.camera.lookAt(this.cameraTarget);
      this.renderer.clear();
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
      text: "three.js",
      bevelEnabled: true,
      font: null,
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
      pointerX: 0,
      pointerXOnPointerDown: 0,
      windowHalfX: window.innerWidth / 2,
    };
  },
};
</script>

<style>
#info {
  position: absolute;
  top: 10px;
  width: 100%;
  text-align: center;
  z-index: 100;
}
</style>
