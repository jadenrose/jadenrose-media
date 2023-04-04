<script>
export default {
    props: ['videoId']
}
</script>

<template>
  <iframe
    class="video-frame"
    :src="`https://www.youtube-nocookie.com/embed/${videoId}`"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen
  ></iframe>
</template>

<style lang="scss">
.video-frame {
  display: block;
  height: 250px;
  width: 100%;
  border-radius: 8px;
}
</style>