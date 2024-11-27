<template>
  <div class="carousel-container">
    <div class="carousel-ring" :style="ringStyle">
      <div 
        v-for="(image, index) in images" 
        :key="index"
        class="carousel-item"
        :class="{ 'active': index === currentIndex }"
        :style="getItemStyle(index)"
        @mouseenter="handleMouseEnter(index)"
        @mouseleave="handleMouseLeave(index)">
        <img :src="image" :alt="`Slide ${index + 1}`" />
      </div>
    </div>
    <button class="carousel-button prev" @click="prevSlide">←</button>
    <button class="carousel-button next" @click="nextSlide">→</button>
  </div>
</template>

<script>
export default {
  name: 'ThreeDCarousel',
  data() {
    return {
      currentIndex: 0,
      images: [
        'https://images.unsplash.com/photo-1441974231531-c6227db76b6e',
        'https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05',
        'https://images.unsplash.com/photo-1447752875215-b2761acb3c5d',
        'https://images.unsplash.com/photo-1465146344425-f00d5f5c8f07',
        '/img/banana.jpg',
        'https://images.unsplash.com/photo-1469474968028-56623f02e42e'
      ],
      rotationY: 0,
      hoveredIndex: null
    }
  },
  computed: {
    anglePerItem() {
      return 360 / this.images.length
    },
    ringStyle() {
      return {
        transform: `rotateY(${this.rotationY}deg)`
      }
    }
  },
  methods: {
    getItemStyle(index) {
      const angle = this.anglePerItem * index
      const radius = 300
      const scale = this.hoveredIndex === index ? 1.3 : 1
      
      return {
        transform: `rotateY(${angle}deg) translateZ(${radius}px) scale(${scale})`,
        zIndex: index === this.currentIndex ? 1 : 0,
        opacity: index === this.currentIndex ? 1 : 0.6
      }
    },
    handleMouseEnter(index) {
      this.hoveredIndex = index
    },
    handleMouseLeave() {
      this.hoveredIndex = null
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length
      this.rotationY -= this.anglePerItem
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length
      this.rotationY += this.anglePerItem
    }
  }
}
</script>

<style scoped>
.carousel-container {
  position: relative;
  width: 100%;
  height: 500px;
  perspective: 1000px;
  overflow: hidden;
}

.carousel-ring {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.carousel-item {
  position: absolute;
  width: 200px;
  height: 200px;
  left: 50%;
  top: 50%;
  margin: -100px 0 0 -100px;
  transition: all 0.3s ease;
  cursor: pointer;
  transform-style: preserve-3d;
}

.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
  transition: all 0.3s ease;
}

.carousel-item.active {
  z-index: 1;
}

.carousel-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.1);
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 25px;
  color: white;
  cursor: pointer;
  font-size: 24px;
  transition: all 0.3s ease;
}

.carousel-button:hover {
  background: transparent;
}

.prev {
  left: 20px;
}

.next {
  right: 20px;
}
</style> 