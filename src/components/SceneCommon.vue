<!--场景渲染模版示例-->

<script setup>
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'; // 导入控制器
import {AxesHelper, Object3D, PerspectiveCamera, Scene, WebGLRenderer} from "three";

const props=defineProps({
  cube: Object3D,
})

/*
* 步骤
* 1.创建场景
* 2.创建相机
* 3.创建渲染器，设置大小，并添加到页面
* 4.创建物体，设置材质，设置网格
* 5.渲染
* */
const scene = new Scene();// 创建场景
const camera = new PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );// 创建透视相机
const renderer = new WebGLRenderer();// 创建渲染器
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
// 设置坐标辅助器
const axesHelper = new AxesHelper( 5 );
scene.add( axesHelper );
// 新建控制器
const controls = new OrbitControls( camera, renderer.domElement );
/* 设置阻尼惯性 */
controls.enableDamping=true
// 设置阻尼系数
controls.dampingFactor=0.03

// 调整相机位置
camera.position.z = 5;
camera.position.y = 2;
camera.position.x = 2;


scene.add(props.cube)

function animate() {
  requestAnimationFrame( animate );
  controls.update();
  renderer.render( scene, camera );
}

animate();

</script>

<template>

</template>

<style>
.canvas{
  display: block;
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
}
</style>
