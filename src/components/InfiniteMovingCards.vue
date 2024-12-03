<template>
  <div class="infinite-cards-container">
    <div class="cards-track" :class="{ 'reverse': direction === 'left', 'pause': isPaused }" :style="{ '--speed': speedMap[speed] }">
      <div class="cards-content">
        <div v-for="(item, index) in items" 
             :key="index" 
             class="card"
             @mouseenter="isPaused = true"
             @mouseleave="isPaused = false">
          <img :src="item.imgSrc" :alt="item.alt" class="card-image">
        </div>
      </div>
      <div class="cards-content" aria-hidden="true">
        <div v-for="(item, index) in items" 
             :key="'duplicate-' + index" 
             class="card"
             @mouseenter="isPaused = true"
             @mouseleave="isPaused = false">
          <img :src="item.imgSrc" :alt="item.alt" class="card-image">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InfiniteMovingCards',
  data() {
    return {
      speedMap: {
        slow: '50s',
        normal: '35s',
        fast: '20s'
      },
      items: [
        { imgSrc: '/img/InfiQue/rdr2.jpg', alt: 'Game Image 1' },
        { imgSrc: '/img/InfiQue/gow.jpg', alt: 'Game Image 2' },
        { imgSrc: '/img/InfiQue/tlou.jpg', alt: 'Game Image 3' },
        { imgSrc: '/img/InfiQue/tlou2.jpg', alt: 'Game Image 4' },
        { imgSrc: '/img/InfiQue/er1.jpg', alt: 'Game Image 5' },
        { imgSrc: '/img/InfiQue/skr.jpg', alt: 'Game Image 6' },
        { imgSrc: '/img/InfiQue/er2.jpg', alt: 'Game Image 7' }
      ],
      isPaused: false
    }
  },
  props: {
    direction: {
      type: String,
      default: 'right'
    },
    speed: {
      type: String,
      default: 'slow'
    }
  }
}
</script>

<style scoped>
.infinite-cards-container {
  width: 100%;
  height: auto;
  overflow: visible;
  position: relative;
  mask-image: linear-gradient(to right, transparent, black 20%, black 80%, transparent);
  -webkit-mask-image: linear-gradient(to right, transparent, black 20%, black 80%, transparent);
}

.cards-track {
  display: flex;
  width: max-content;
  animation: scroll var(--speed) linear infinite;
  position: relative;
}

.cards-track.reverse {
  animation-direction: reverse;
}

.cards-track.pause {
  animation-play-state: paused;
}

.cards-content {
  display: flex;
  gap: 2rem;
  padding: 1rem;
  position: relative;
}

.card {
  flex-shrink: 0;
  width: 300px;
  height: 200px;
  border-radius: 0.5rem;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  position: relative;
  z-index: 1;
  transform-origin: center;
}

.card:hover {
  transform: scale(1.15);
  z-index: 100;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 0.5rem;
  transition: all 0.3s ease;
}

.card:hover .card-image {
  border-radius: 0.5rem;
}

@keyframes scroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(calc(-50% - 1rem));
  }
}

@media (prefers-reduced-motion: reduce) {
  .cards-track {
    animation-play-state: paused;
  }
}
</style> 