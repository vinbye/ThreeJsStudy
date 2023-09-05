<template>

</template>

<script setup>
import * as THREE from "three"
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'; // 导入控制器

const scene = new THREE.Scene();// 创建场景
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );// 创建透视相机
const renderer = new THREE.WebGLRenderer();// 创建渲染器
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );


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
const bufferMaterial = new THREE.MeshBasicMaterial( { color: 0xff0000,side:THREE.DoubleSide } );
const mesh = new THREE.Mesh( bufferGeometry, bufferMaterial );

scene.add(mesh)

// 调整相机位置
camera.position.z = 5;
camera.position.y = 2;
camera.position.x = 2;
// 新建控制器
const controls = new OrbitControls( camera, renderer.domElement );
// 设置坐标辅助器
const axesHelper = new THREE.AxesHelper( 5 );
scene.add( axesHelper );

/* 设置阻尼惯性 */
controls.enableDamping=true
// 设置阻尼系数
controls.dampingFactor=0.03

function animate() {
  requestAnimationFrame( animate );
  controls.update();
  renderer.render( scene, camera );
}

animate();
</script>

<style  lang="scss" src="../assets/common.scss">

</style>
