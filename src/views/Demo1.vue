<template></template>

<script setup>
import * as THREE from "three"
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'; // 导入控制器
/*
* 步骤
* 1.创建场景
* 2.创建相机
* 3.创建渲染器，设置大小，并添加到页面
* 4.创建物体，设置材质，设置网格
* 5.渲染
* */
const scene = new THREE.Scene();// 创建场景
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );// 创建透视相机
const renderer = new THREE.WebGLRenderer();// 创建渲染器
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

/* 创建立方体 */
const parentGeometry=new THREE.BoxGeometry(1,1,1);
const parentMaterial=new THREE.MeshBasicMaterial({color:0xff0000})
const parentCube=new THREE.Mesh(parentGeometry,parentMaterial);
/* 设置物体坐标 */
parentCube.position.set(-2,0,0); // 坐标平移
// parentCube.scale.set(1,2,1)

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
/* 使用材质 */
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
/* 子元素设置的物体坐标是相对父元素的坐标设定的 */
cube.position.set(2,0,0)
// cube.scale.set(2,2,1); // 坐标缩放，也是相对父元素而言
cube.rotation.x=Math.PI/4; // 绕x轴旋转45度

parentCube.add(cube);// 父元素增加子元素
scene.add( parentCube );
// 设置坐标辅助器
const axesHelper = new THREE.AxesHelper( 5 );
scene.add( axesHelper );

// 调整相机位置
camera.position.z = 5;
camera.position.y = 2;
camera.position.x = 2;
// 新建控制器
const controls = new OrbitControls( camera, renderer.domElement );
/* 设置阻尼惯性 */
controls.enableDamping=true
// 设置阻尼系数
controls.dampingFactor=0.03


function animate() {
  requestAnimationFrame( animate );
  controls.update();

  // cube.rotation.x += 0.01;
  // cube.rotation.y += 0.01;
  renderer.render( scene, camera );

}
animate();
</script>

<style lang="scss" src="../assets/common.scss"></style>
