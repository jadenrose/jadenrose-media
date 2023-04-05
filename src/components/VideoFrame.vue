<script setup>
import { reactive, onMounted, onUnmounted } from 'vue';

const state = reactive({ dots: 3 })

let interval

onMounted(() => {
    interval = setInterval(() => {
        if (state.dots === 3) state.dots = 1
        else state.dots++
    }, 300)

})

onUnmounted(() => {
    clearInterval(interval)
})

const handleVideoReady = () => {
    console.log('video ready')
}

</script>

<script>

export default {
    props: ['videoId']
}
</script>

<template>
  <div class="video-wrapper">
    <iframe
      class="video-frame"
      :src="`https://www.youtube-nocookie.com/embed/${videoId}`"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
      allowfullscreen
    >
    </iframe>
    <div class="video-fallback">
      <span>
        <span class="text">YouTube Embeds{{ '.'.repeat(state.dots) }}</span>
        <span class="turtle">🐢</span>
      </span>
    </div>
  </div>
</template>

<style lang="scss">
.video-wrapper,
.video-frame {
  display: block;
  height: 250px;
  width: 100%;
  border-radius: 8px;
}

.video-wrapper {
  position: relative;
  z-index: 0;
  overflow: hidden;
}

.video-fallback {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: $black;
  z-index: -1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.video-fallback .text {
  display: inline-block;
  width: 16ch;
}

.turtle {
  font-size: 2rem;
}
</style>