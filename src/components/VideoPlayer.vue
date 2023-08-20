<script setup lang="ts">
import { ref, computed } from 'vue'

const videoRef = ref<HTMLVideoElement | null>(null)

let paused = ref<boolean>(false)

const togglePaused = () => {
  paused.value = !paused.value
}

const onVideoEnded = () => {
  // Handle the video ended event here
  console.log('onVideoEnded')
}

const play = () => {
  if (videoRef.value) {
    videoRef.value?.play()
    togglePaused()
  }
}

const pause = () => {
  if (videoRef.value) {
    videoRef.value?.pause()
    togglePaused()
  }
}

const mute = () => {
  if (videoRef.value) {
    videoRef.value!.muted = !videoRef.value?.muted
  }
}

const BUTTONS = computed(() => [
  {
    name: paused.value ? 'play' : 'pause',
    label: paused.value ? 'Play' : 'Pause',
    className: 'play-pause',
    click: () => paused.value ? play() : pause()
  },
  {
    name: 'mute',
    label: 'Mute',
    click: () => mute()
  },
])
</script>

<template>
  <div class="video-container">
    <video
      class="video"
      ref="videoRef"
      v-bind="$attrs"
      @ended="onVideoEnded"
    >
      Your browser does not support the video tag.
    </video>
    <div class="buttons">
      <button
        v-for="{ name, label, click, className } in BUTTONS"
        :key="name"
        class="button"
        :class="className"
        @click="click"
      >
        {{label}}
      </button>
    </div>
  </div>
</template>

<style>
.video-container {
  position: relative;
}

.video {
  width: 100vw;
  height: 100vh;
  object-fit: contain;
}

.buttons {
  position: absolute;
  right: 20px;
  bottom: 60px;
  display: grid;
  grid-auto-flow: column;
  column-gap: .8rem;
}

.button {
  padding: .4rem 1.2rem;
  background-color: var(--color-background-soft);
  color: var(--vt-c-white);
  border: none;
  border-radius: .4rem;
  cursor: pointer;
  box-shadow: 0 0 3px var(--vt-c-white);
}

.play-pause {
  width: 80px;
}
</style>
