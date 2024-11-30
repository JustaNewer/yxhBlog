<template>
  <div class="relative flex h-[500px] w-full flex-col items-center justify-center overflow-hidden rounded-lg">
    <!-- First row -->
    <div class="marquee-track" :class="{ 'pause': pauseOnHover }">
      <div class="marquee-content" :style="{ '--duration': duration }">
        <div v-for="(image, index) in firstRow" :key="index" class="game-card">
          <img :src="image.src" :alt="image.alt" class="game-image">
        </div>
        <div v-for="(image, index) in firstRow" :key="'duplicate-' + index" class="game-card">
          <img :src="image.src" :alt="image.alt" class="game-image">
        </div>
      </div>
    </div>

    <!-- Second row -->
    <div class="marquee-track" :class="{ 'pause': pauseOnHover }">
      <div class="marquee-content reverse" :style="{ '--duration': duration }">
        <div v-for="(image, index) in secondRow" :key="index" class="game-card">
          <img :src="image.src" :alt="image.alt" class="game-image">
        </div>
        <div v-for="(image, index) in secondRow" :key="'duplicate-' + index" class="game-card">
          <img :src="image.src" :alt="image.alt" class="game-image">
        </div>
      </div>
    </div>

    <!-- Gradient overlays -->
    <div class="pointer-events-none absolute inset-y-0 left-0 w-1/3 bg-gradient-to-r from-[#1a1a1a]"></div>
    <div class="pointer-events-none absolute inset-y-0 right-0 w-1/3 bg-gradient-to-l from-[#1a1a1a]"></div>
  </div>
</template>

<script>
export default {
  name: 'GameMarquee',
  data() {
    return {
      gameImages: [
        { src: '/public/img/steam2.png', alt: 'Game 1' },
        { src: '/img/psSymbol.jpg', alt: 'Game 2' },
        { src: '/img/psSymbol.jpg', alt: 'Game 3' },
        { src: '/img/psSymbol.jpg', alt: 'Game 4' },
        { src: '/img/psSymbol.jpg', alt: 'Game 5' },
        { src: '/img/psSymbol.jpg', alt: 'Game 6' },
      ],
      duration: '20s',
      pauseOnHover: true
    }
  },
  computed: {
    firstRow() {
      return this.gameImages.slice(0, Math.ceil(this.gameImages.length / 2))
    },
    secondRow() {
      return this.gameImages.slice(Math.ceil(this.gameImages.length / 2))
    }
  }
}
</script>

<style scoped>
.marquee-track {
  width: 100%;
  overflow: hidden;
  padding: 1rem 0;
}

.marquee-content {
  display: inline-flex;
  animation: scroll var(--duration) linear infinite;
  gap: 1rem;
}

.game-card {
  flex: 0 0 auto;
  width: 300px;
  height: 200px;
  overflow: hidden;
  border-radius: 0.75rem;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.game-card:hover {
  transform: scale(1.05);
}

.game-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.reverse {
  animation-direction: reverse;
}

.pause:hover .marquee-content {
  animation-play-state: paused;
}

@keyframes scroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(calc(-100% - 1rem));
  }
}

.pointer-events-none {
  pointer-events: none;
}

.absolute {
  position: absolute;
}

.inset-y-0 {
  top: 0;
  bottom: 0;
}

.left-0 {
  left: 0;
}

.right-0 {
  right: 0;
}

/* .w-1/3 {
  width: 33.333333%;
} */

.bg-gradient-to-r {
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
}

.bg-gradient-to-l {
  background-image: linear-gradient(to left, var(--tw-gradient-stops));
}

.from-\[\#1a1a1a\] {
  --tw-gradient-from: #1a1a1a;
  --tw-gradient-stops: var(--tw-gradient-from), transparent;
}

.relative {
  position: relative;
}

.flex {
  display: flex;
}

.h-\[500px\] {
  height: 500px;
}

.w-full {
  width: 100%;
}

.flex-col {
  flex-direction: column;
}

.items-center {
  align-items: center;
}

.justify-center {
  justify-content: center;
}

.overflow-hidden {
  overflow: hidden;
}

.rounded-lg {
  border-radius: 0.5rem;
}
</style>