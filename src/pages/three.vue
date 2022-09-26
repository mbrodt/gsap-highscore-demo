<template>
  <canvas id="canvas"></canvas>
</template>

<script setup>
import { onMounted } from "vue";
import * as THREE from "three";
onMounted(() => {
  let INTERSECTED;

  const pointer = new THREE.Vector2();
  const raycaster = new THREE.Raycaster();

  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  document.addEventListener("mousemove", onPointerMove);

  function onPointerMove(event) {
    pointer.x = (event.clientX / window.innerWidth) * 2 - 1;
    pointer.y = -(event.clientY / window.innerHeight) * 2 + 1;
  }

  const renderer = new THREE.WebGLRenderer({
    canvas: document.querySelector("#canvas"),
  });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  const cubes = [
    new THREE.Mesh(
      new THREE.BoxGeometry(1, 1, 1),
      new THREE.MeshBasicMaterial({ color: 0xff0000 })
    ),
    new THREE.Mesh(
      new THREE.BoxGeometry(1, 1, 1),
      new THREE.MeshBasicMaterial({ color: 0x00ff00 })
    ),
    new THREE.Mesh(
      new THREE.BoxGeometry(1, 1, 1),
      new THREE.MeshBasicMaterial({ color: 0x0000ff })
    ),
  ];

  cubes.forEach((cube, i) => {
    cube.position.x = (i - 1) * 2;
    console.log(cube.material.color);
    cube.name = "cube";
    scene.add(cube);
  });
  // camera.lookAt(cube.position);
  camera.position.y = 1;
  camera.position.z = 4;

  // scene.add(new THREE.AxesHelper(5));
  console.log(scene);

  function animate() {
    requestAnimationFrame(animate);

    raycaster.setFromCamera(pointer, camera);

    const intersects = raycaster.intersectObjects(scene.children, false);
    if (intersects.length > 0) {
      if (INTERSECTED != intersects[0].object) {
        INTERSECTED = intersects[0].object;
        INTERSECTED.currentColor = INTERSECTED.material.color.getHex();
        INTERSECTED.material.color.setHex(0xffffff);
      }
    } else {
      if (INTERSECTED) {
        console.log("INTERSECTED in else:", INTERSECTED);
        INTERSECTED.material.color.setHex(INTERSECTED.currentColor);
        INTERSECTED = null;
      }
    }

    renderer.render(scene, camera);
  }
  animate();
});
</script>

<style lang="scss" scoped></style>
