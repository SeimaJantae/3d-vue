<script setup lang="ts">
import { ACESFilmicToneMapping, Color, SRGBColorSpace } from "three";
import { TresCanvas } from "@tresjs/core";
import { Environment, OrbitControls, GLTFModel } from "@tresjs/cientos";

import { useProgress } from "@tresjs/cientos";

const { hasFinishLoading, progress } = await useProgress();

const gl = {
  antialias: true,
  alpha: true,
  powerPreference: "high-performance",
  toneMapping: ACESFilmicToneMapping,
  toneMappingExposure: 1,
  outputColorSpace: SRGBColorSpace,
  // pixelRatio: Math.min(window.devicePixelRatio, 2)
};
</script>

<template>
  <Transition
    name="fade-overlay"
    enter-active-class="opacity-1 transition-opacity duration-200"
    leave-active-class="opacity-0 transition-opacity duration-200"
  >
    <div
      v-show="!hasFinishLoading"
      class="absolute bg-grey-600 t-0 l-0 w-full h-full z-20 flex justify-center items-center text-black font-mono"
    >
      <div class="w-200px">
        Loading... {{ progress }} %
        <i class="i-ic-twotone-catching-pokemon animate-rotate-in"></i>
      </div>
    </div>
  </Transition>

  <Suspense>
    <TresCanvas v-bind="gl" window-size>
      <TresPerspectiveCamera :position="[-4.8996821449561825, 1.1559522738747594, 6.374315294125424]" />
      <OrbitControls
        :enableDamping="true"
        :enable-pan="false"
        :enable-zoom="true"
        :min-polar-angle="1.1"
        :max-polar-angle="Math.PI / 2.2"
        :min-distance="3"
        :max-distance="7"
      />

      <!-- if uncommnet this glb can render all -->
      <!-- <Suspense>
        <GLTFModel
          path="https://raw.githubusercontent.com/Tresjs/assets/main/models/gltf/blender-cube.glb"
          :scale="[0, 0, 0]"
        />
      </Suspense> -->

      <Suspense>
        <GLTFModel path="/assets/10177.glb" draco />
      </Suspense>

      <Suspense>
        <GLTFModel path="/assets/10177_Mercedes_OE_001.glb" draco />
      </Suspense>

      <Suspense>
        <GLTFModel path="/assets/freight_station_BG_01.glb" draco />
      </Suspense>

      <Suspense>
        <Environment :background="false" files="/assets/freight_station_2k.hdr" />
      </Suspense>
    </TresCanvas>
  </Suspense>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
#app {
  height: 100%;
  width: 100%;
}
</style>
