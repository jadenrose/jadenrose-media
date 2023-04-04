<script setup>
import { reactive } from 'vue';
import SongTag from '@/components/SongTag.vue';

const state = reactive({ selectedIndex: -1, selectedDescription: null })

const setDescription = (description) => {
    state.selectedDescription = description
}

const setSelectedIndex = (index) => {
    state.selectedIndex = index
}
</script>

<script>
export default {
    props: ["tags"]
}
</script>

<template>
  <div class="tags-list">
    <SongTag
      v-for="({ label, description }, index) in tags"
      :label="label"
      :description="description"
      :isCurrentlySelected="index === state.selectedIndex"
      @click="
        () => {
          if (index === state.selectedIndex) {
            setDescription(null)
            setSelectedIndex(-1)
          } else {
            setDescription(description)
            setSelectedIndex(index)
          }
        }
      "
    />
  </div>
  <div class="tag-description" v-if="state.selectedDescription">
    <button
      class="hide-tag-button"
      @click="
        () => {
          setDescription(null)
          setSelectedIndex(-1)
        }
      "
    >
      Hide
    </button>
    <p v-html="state.selectedDescription" />
  </div>
</template>

<style lang="scss">
.tags-list {
  display: flex;
}

.tag-description {
  position: relative;
  margin-top: 8px;
  background: $color;
  color: $background;
  border-radius: 8px;
  width: 67%;
  padding-top: 0px;
  font-size: 14px;
  padding: 12px;
  padding-top: 40px;
}

.tag-description p {
  margin-bottom: 0;
}

.tag-description a {
  display: inline-block;
  color: inherit;
  font-weight: bold;
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