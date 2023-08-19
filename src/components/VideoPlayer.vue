<script setup lang="ts">
import { ref, } from 'vue'

const videoRef = ref<HTMLVideoElement | null>(null)

const onVideoEnded = () => {
  // Handle the video ended event here
  console.log('onVideoEnded')
}

const play = () => {
  if (videoRef.value) {
    videoRef.value?.play()
  }
}

const pause = () => {
  if (videoRef.value) {
    videoRef.value?.pause()
  }
}

const mute = () => {
  if (videoRef.value) {
    videoRef.value!.muted = !videoRef.value?.muted
  }
}

const BUTTONS = [
  {
    name: 'play',
    label: 'Play',
    click: () => play()
  },
  {
    name: 'pause',
    label: 'Pause',
    click: () => pause()
  },
  {
    name: 'mute',
    label: 'Mute',
    click: () => mute()
  },
]
</script>

<template>
  <div>
    <suspense>
      <video ref="videoRef" v-bind="$attrs" @ended="onVideoEnded">
        Your browser does not support the video tag.
      </video>
    </suspense>
    <div>
      <button v-for="{ name, label, click } in BUTTONS" :key="name" @click="click">{{label}}</button>
    </div>
  </div>
</template>
