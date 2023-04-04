<script setup>
import VideoFrame from "./VideoFrame.vue";
import SongTags from './SongTags.vue';
</script>

<script>
export default {
    props: ["song"],
    components: { VideoFrame, SongTags }
}
</script>

<template>
  <article class="song">
    <div class="song-content">
      <h2 class="song-headline" v-if="song.headline">
        {{ song.headline }}
      </h2>
      <p class="song-name" v-if="song.songName">
        Song name: {{ song.songName }}
        <span class="song-name-info" v-if="song.songNameInfo">🛈</span>
      </p>
      <p class="song-body" v-if="song.body">{{ song.body }}</p>
      <p>Technology Shoutouts:</p>
      <SongTags :tags="song.technologyShoutouts" />
    </div>
    <VideoFrame v-if="song.videoId" :videoId="song.videoId" />
  </article>
</template>

<style lang="scss">
.song {
  margin-bottom: $space-between-sections;
  display: grid;
  grid-template-columns: 5fr 4fr;
  column-gap: 32px;
  align-items: center;
}

.song-headline {
  font-size: 32px;
  line-height: 1;
  margin-bottom: 18px;
}

.song-name-info {
  cursor: pointer;
}
</style>