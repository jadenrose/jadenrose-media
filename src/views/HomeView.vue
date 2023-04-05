<script setup>
import content from '@/assets/content.json'
import Song from '@/components/Song.vue'
import Navbar from '../components/Navbar.vue'
import Footer from '../components/Footer.vue'
</script>

<template>
  <Navbar />
  <div class="page-container">
    <main class="page-main">
      <section class="intro-section">
        <h1
          class="page-headline"
          v-if="content.headline"
          v-html="content.headline"
        />
        <p class="page-subheadline" v-if="content.headline">
          {{ content.subheadline }}
        </p>
        <p class="preamble-item" v-for="item in content.preamble">{{ item }}</p>
      </section>
      <section class="songs-section">
        <Song v-for="song in content.songs" :song="song" />
      </section>
    </main>
  </div>
  <Footer />
</template>

<style lang="scss">
.page-container {
  padding-left: 5vw;
  padding-right: 5vw;
}

.page-main {
  margin-top: 11.11rem;
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
}

.page-headline {
  font-size: 3.11rem;
  line-height: 3.11rem;
  margin-bottom: 24px;
}

.page-subheadline {
  font-size: 1.78rem;
  line-height: 1;
  margin-bottom: 48px;
}

.intro-section {
  margin-bottom: $space-between-sections;
}
</style>
