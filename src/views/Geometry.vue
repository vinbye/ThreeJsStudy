
<template>
  <SceneCommon :cube="cube"></SceneCommon>
</template>


<script setup>
import SceneCommon from "../components/SceneCommon.vue";

import * as THREE from "three";

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );
const material1 = new THREE.MeshBasicMaterial( {color: 0xff0000} );
const material2 = new THREE.MeshBasicMaterial( {color: 0x0000ff} );
const material3 = new THREE.MeshBasicMaterial( {color: 0xf0f0f0} );
const material4 = new THREE.MeshBasicMaterial( {color: 0xe342c1} );
const material5 = new THREE.MeshBasicMaterial( {color: 0x23dc43} );
const cube = new THREE.Mesh( geometry, [material,material1,material2,material3,material4,material5] );
</script>

