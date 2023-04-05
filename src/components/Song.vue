<script setup>
import VideoFrame from './VideoFrame.vue'
import SongTags from './SongTags.vue'
import { reactive } from 'vue'

const props = defineProps(['song'])
const state = reactive({ showSongInfo: false })

const handleToggleSongInfo = () => {
  if (props.song.songNameInfo) state.showSongInfo = !state.showSongInfo
}

const handleHideSongInfo = () => {
  if (props.song.songNameInfo) state.showSongInfo = false
}
</script>

<template>
  <article class="song">
    <div class="song-content">
      <h2 class="song-headline" v-if="song.headline">
        {{ song.headline }}
      </h2>
      <p
        class="song-name"
        :class="{ 'has-info': song.songNameInfo }"
        v-if="song.songName"
        @click="handleToggleSongInfo"
      >
        Song name: {{ song.songName }}
        <svg
          v-if="song.songNameInfo"
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          viewBox="0 0 24 24"
        >
          <path
            fill="currentColor"
            d="M11 17h2v-6h-2v6Zm1-8q.425 0 .713-.288T13 8q0-.425-.288-.713T12 7q-.425 0-.713.288T11 8q0 .425.288.713T12 9Zm0 13q-2.075 0-3.9-.788t-3.175-2.137q-1.35-1.35-2.137-3.175T2 12q0-2.075.788-3.9t2.137-3.175q1.35-1.35 3.175-2.137T12 2q2.075 0 3.9.788t3.175 2.137q1.35 1.35 2.138 3.175T22 12q0 2.075-.788 3.9t-2.137 3.175q-1.35 1.35-3.175 2.138T12 22Zm0-2q3.35 0 5.675-2.325T20 12q0-3.35-2.325-5.675T12 4Q8.65 4 6.325 6.325T4 12q0 3.35 2.325 5.675T12 20Zm0-8Z"
          />
        </svg>
      </p>
      <div
        class="song-name-info"
        v-if="state.showSongInfo && song.songNameInfo"
      >
        <button class="hide-tag-button" @click="handleHideSongInfo">
          Hide
        </button>
        <p v-html="song.songNameInfo" />
      </div>
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

  @include tablet {
    display: grid;
    grid-template-columns: 5fr 4fr;
    column-gap: 32px;
    align-items: center;
  }
}

.song-content {
  margin-bottom: 24px;
}

.song-headline {
  font-size: 1.78rem;
  line-height: 1;
  margin-bottom: 18px;
}

.song-name.has-info {
  cursor: pointer;
  user-select: none;
}

.song-name-info {
  position: relative;
  display: inline-block;
  font-size: 0.78rem;
  background: $color;
  color: $background;
  padding: 8px;
  border-radius: 8px;
  margin-bottom: 18px;

  @include tablet {
    width: 67%;
  }
}

.hide-tag-button {
  @include button-reset;

  font-weight: bold;
  background: $background;
  color: $color;
  border-radius: 8px;
  padding: 4px 8px;
  display: inline-block;
  position: absolute;
  top: 8px;
  right: 8px;
}

.hide-tag-button:hover {
  background: $background-hover;
}
</style>
