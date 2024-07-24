<script setup lang="ts">

import { useGLTF } from '@tresjs/cientos'

// const props = defineProps<{
//   // modelFile: string
//   // carId: string
//   // setDots: Function
//   // scene: any
//   // model: any
// }>()

const { scene, nodes, animations, materials } = await useGLTF('/assets/10177.glb', {
  draco: true
})

console.log('scene car', scene)
</script>

<template>
  <TresDirectionalLight
    :position="[0.4, -0.3, -8.4]"
    :intensity="0.3"
    :cast-shadow="false"
  ></TresDirectionalLight>
  <primitive :object="scene" />
</template>
