<script setup>
import { reactive, onMounted, onUnmounted } from 'vue'

const state = reactive({ navbarVisible: true })

let previousScrollPosition = 0
let currentScrollPosition = 0
let ticking = false

const handleScroll = (current, previous) => {
  if (current < previous) {
    state.navbarVisible = true
  } else {
    if (current > 100) state.navbarVisible = false
    else state.navbarVisible = true
  }

  previousScrollPosition = current
}

const throttleScroll = () => {
  currentScrollPosition = window.scrollY

  if (!ticking) {
    window.requestAnimationFrame(() => {
      handleScroll(currentScrollPosition, previousScrollPosition)
      ticking = false
    })

    ticking = true
  }
}

onMounted(() => {
  document.addEventListener('scroll', throttleScroll)
})

onUnmounted(() => {
  document.removeEventListener('scroll', throttleScroll)
})
</script>

<template>
  <header class="navbar" :class="{ visible: state.navbarVisible }">
    <a
      class="navbar-pill"
      href="https://www.youtube.com/channel/UCyF48y9NK43P2gTJ5K0WwpQ"
      target="_blank"
      rel="noreferrer"
    >
      <span class="pill-child">JADEN ROSE</span>
      <span class="pill-child">MEDIA</span>
    </a>
  </header>
</template>

<style lang="scss">
.navbar {
  padding: 48px 5vw;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;

  @include tablet {
    justify-content: space-between;
  }

  transform: translateY(-110%);
  transition: transform 0.2s ease-out;
}

.navbar.visible {
  transform: translateY(0%);
}

.navbar-pill {
  display: inline-flex;
  gap: 4px;
  font-size: 1.33rem;
  font-weight: bold;
  text-decoration: none;
  background: $background;
  border-radius: 14px;
  box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.8);
  padding: 3px;
}

.pill-child {
  display: inline-block;
  background: $color;
  color: $background;
  padding: 8px;
}

.pill-child:first-child {
  border-radius: 12px 0 0 12px;
}

.pill-child:nth-child(2) {
  border-radius: 0 12px 12px 0;
}
</style>
