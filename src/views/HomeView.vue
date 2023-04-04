<script setup>
import content from '@/assets/content.json'
import Song from '@/components/Song.vue'
</script>

<template>
  <main class="page-main">
    <section class="intro-section">
      <h1 class="page-headline" v-if="content.headline" v-html="content.headline" />
      <p class="page-subheadline" v-if="content.headline">{{ content.subheadline }}</p>
      <p class="preamble-item" v-for="item in content.preamble">{{ item }}</p>
    </section>
    <section class="songs-section">
      <Song v-for="song in content.songs" :song="song" />
    </section>
  </main>
</template>

<style lang="scss">
.page-main {
  margin-top: 200px;
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
}

.page-headline {
  font-size: 56px;
  line-height: 56px;
  margin-bottom: 24px;
}

.page-subheadline {
  font-size: 32px;
  line-height: 1;
  margin-bottom: 48px;
}

.intro-section {
  margin-bottom: $space-between-sections;
}
</style>
