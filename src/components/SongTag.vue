<script>
export default {
  props: ['label', 'description', 'isCurrentlySelected'],
}
</script>

<template>
  <div class="song-tag" :class="{ selected: isCurrentlySelected }">
    <span class="song-tag-label">{{ label }}</span>
    <span class="song-tag-show">Show</span>
  </div>
</template>

<style lang="scss">
.song-tag {
  user-select: none;
  position: relative;
  overflow: hidden;
  background: $color;
  color: $background;
  padding: 4px 8px;
  border-radius: 8px;
  margin-right: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  font-weight: bold;
  font-size: 0.78rem;
  margin-bottom: 8px;
}

.song-tag.selected {
  box-shadow: 0 0 0 3px $accent;
}

.song-tag-show {
  user-select: none;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: $color;
  opacity: 0;
  transition: opacity 0.1s;
}

.song-tag-show:hover {
  opacity: 1;
}
</style>
