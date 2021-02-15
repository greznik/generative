<template>
  <canvas ref="svg"></canvas>
</template>

<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";

export default {
  name: "Svg",
  data() {
    const scene = new THREE.Scene();
    const renderer = null;
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      1,
      3000
    );
    const light = new THREE.DirectionalLight(0xffffff);
    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const texture = new THREE.TextureLoader().load("../../assets/svg_morphing");
    const material = new THREE.PointCloudMaterial({
      size: 5,
      vertexColors: THREE.VertexColors,
      map: texture,
      alphaTest: 0.5,
    });
    const pointCloud = new THREE.PointCloud(geometry, material);
    const images = ["img/github.svg", "img/comment.svg", "img/clock.svg"];
    return {
      scene,
      renderer,
      camera,
      light,
      geometry,
      material,
      texture,
      pointCloud,
      images,
    };
  },
  mounted() {
    const canvas = this.$refs.svg;
    const ctx = canvas.getContext("2d");
    this.renderer = new THREE.WebGLRenderer({
      antialias: true,
      canvas: canvas,
    });
    this.renderer.setSize(window.innerWidth, window.innerHeight);

    this.camera.position.set(0, 0, 2);
    this.light.position.set(0, 0, 10);
    this.scene.add(this.light);

    window.addEventListener("resize", this.onWindowResize, false);

    this.animate();
    this.init();
  },
  methods: {
    loadImages(paths, whenLoaded) {
      let imgs = [];
      paths.forEach((path) => {
        let img = new Image();
        img.onload = () => {
          imgs.push(img);
          if (imgs.length == paths.length) whenLoaded(imgs);
        };
        img.src = path;
      });
    },
    fillUp(array, max) {
      let length = array.length;
      for (let i = 0; i < max - length; i++) {
        array.push(array[Math.floor(Math.random() * length)]);
      }
      return array;
    },
    shuffle(a) {
      for (let i = a.length; i; i--) {
        let j = Math.floor(Math.random() * i);
        [a[i - 1], a[j]] = [a[j], a[i - 1]];
      }
      return a;
    },
    getArrayFromImage(img) {
      let imageCoords = [];
      ctx.clearRect(0, 0, size, size);
      ctx.drawImage(img, 0, 0, size, size);
      let data = ctx.getImageData(0, 0, size, size);

      data = data.data;

      for (let y = 0; y < size; y++) {
        for (let x = 0; x < size; x++) {
          let red = data[(size * y + x) * 4];
          let green = data[(size * y + x) * 4 + 1];
          let blue = data[(size * y + x) * 4 + 2];
          let alpha = data[(size * y + x) * 4 + 3];
          if (alpha > 0) {
            imageCoords.push([10 * (x - size / 2), 10 * (size / 2 - y)]);
          }
        }
      }
      return this.shuffle(this.fillUp(imageCoords, 1500));
    },
  },
};
</script>
