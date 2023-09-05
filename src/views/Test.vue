<template>
  <SceneCommon :cube="mesh"></SceneCommon>
</template>

<script setup>
import * as THREE from "three"
import SceneCommon from "../components/SceneCommon.vue";
import {DoubleSide} from "three";


const bufferGeometry = new THREE.BufferGeometry();
// 定点的逆时针为正面，顺时针为反面
const vertices = new Float32Array( [
  -1.0, -1.0, 0,
  1.0, -1.0,  0,
  1.0,  1.0,  0,
  -1.0,  1.0,  0,
] );

// itemSize = 3 因为每个顶点都是一个三元组。
bufferGeometry.setAttribute( 'position', new THREE.BufferAttribute( vertices, 3 ) );

const indices=new Uint16Array([0,1,2,2,3,0])

// 创建索引属性
bufferGeometry.setIndex(new THREE.BufferAttribute(indices,1))
// 设置两个顶点组，形成两个材质

bufferGeometry.addGroup(0,3,0);
bufferGeometry.addGroup(3,3,1);


console.log( bufferGeometry)

const bufferMaterial = new THREE.MeshBasicMaterial( { color: 0xff0000,side:DoubleSide} );
const bufferMaterial1 = new THREE.MeshBasicMaterial( { color: 0x00ff00,side:DoubleSide,wireframe:true} );


const mesh = new THREE.Mesh( bufferGeometry, [bufferMaterial,bufferMaterial1] );



</script>

<style  lang="scss" src="../assets/common.scss">

</style>
