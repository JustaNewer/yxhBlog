<template>
  <div class="testimonials-container">
    <div class="testimonials-wrapper">
      <div class="stacked-images">
        <div 
          v-for="(testimonial, index) in testimonials" 
          :key="index"
          class="image-card"
          :class="{ 
            'active': currentIndex === index,
            'behind': index < currentIndex,
            'front': index > currentIndex 
          }"
          :style="{ zIndex: getZIndex(index) }"
        >
          <img :src="testimonial.url" :alt="testimonial.title" />
        </div>
      </div>
      
      <div class="text-content">
        <div class="fixed-title">
          <span>The most</span>
          <span class="attribute" :key="testimonials[currentIndex].attribute">{{ testimonials[currentIndex].attribute }}</span>
          <span>game I played</span>
        </div>
        
        <div 
          v-for="(testimonial, index) in testimonials" 
          :key="index"
          class="dynamic-content"
          :class="{ 'active': currentIndex === index }"
        >
          <p class="quote">
            "<TypingAnimation 
              :text="testimonial.description"
              :key="currentIndex"
            />"
          </p>
          <div class="author-details">
            <a :href="testimonial.link" target="_blank" class="name">{{ testimonial.title }}</a>
            <span class="designation">Available on Steam/PlayStation</span>
          </div>
        </div>
      </div>
    </div>
    
    <div class="navigation-arrows">
      <button class="arrow-btn prev" @click="prevTestimonial" :disabled="currentIndex === 0">←</button>
      <button class="arrow-btn next" @click="nextTestimonial" :disabled="currentIndex === testimonials.length - 1">→</button>
    </div>
  </div>
</template>

<script>
import TypingAnimation from './TypingAnimation.vue'

export default {
  name: 'AnimatedTestimonials',
  components: {
    TypingAnimation
  },
  data() {
    return {
      currentIndex: 0,
      autoPlayInterval: null,
      testimonials: [
        {
          attribute: 'PAINFUL',
          description: 'A challenging masterpiece that tests your skills and patience. Every victory feels earned through blood, sweat, and tears.',
          title: 'Sekiro',
          link: 'https://store.steampowered.com/app/814380/Sekiro_Shadows_Die_Twice__GOTY_Edition/',
          url: '/img/games/sekiro.png'
        },
        {
          attribute: 'REAL',
          description: 'An epic tale of honor and loyalty in the dying days of the outlaw age. Experience the story of Arthur Morgan in this acclaimed open-world adventure.',
          title: 'Red Dead Redemption 2',
          link: 'https://store.steampowered.com/app/1174180/Red_Dead_Redemption_2/',
          url: '/img/games/rdr.jpg'
        },
        {
          attribute: 'EMOTIONAL',
          description: 'A gripping story of survival and love. The emotional journey of Joel and Ellie will stay with you long after the credits roll.',
          title: 'The Last of Us',
          link: 'https://www.playstation.com/en-sg/games/the-last-of-us-part-i/',
          url: '/img/games/tlou.jpg'
        },
        {
          attribute: 'EPIC',
          description: 'Journey through Norse realms with Kratos and Atreus in this emotional tale of father and son, featuring intense combat and stunning visuals.',
          title: 'God of War',
          link: 'https://www.playstation.com/en-sg/games/god-of-war-ragnarok/',
          url: '/img/games/gow.jpg'
        },
        {
          attribute: 'WORTHBUY',
          description: 'Rise, Tarnished, and explore a vast open world filled with epic battles, mysterious stories, and challenging dungeons.',
          title: 'Elden Ring',
          link: 'https://store.steampowered.com/app/1245620/Elden_Ring/',
          url: '/img/games/elden.png'
        }
      ]
    }
  },
  methods: {
    prevTestimonial() {
      if (this.currentIndex > 0) {
        this.currentIndex--
      }
    },
    nextTestimonial() {
      if (this.currentIndex < this.testimonials.length - 1) {
        this.currentIndex++
      } else {
        // Reset to first slide when reaching the end
        this.currentIndex = 0
      }
    },
    getZIndex(index) {
      return this.testimonials.length - Math.abs(this.currentIndex - index)
    },
    startAutoPlay() {
      this.autoPlayInterval = setInterval(() => {
        this.nextTestimonial()
      }, 5000) // Change slide every 5 seconds
    },
    stopAutoPlay() {
      if (this.autoPlayInterval) {
        clearInterval(this.autoPlayInterval)
      }
    }
  },
  mounted() {
    this.startAutoPlay()
  },
  beforeUnmount() {
    this.stopAutoPlay()
  }
}
</script>

<style scoped>
.testimonials-container {
  position: relative;
  width: 800px;
  height: 300px;
  margin-left: 50px;
  margin-top: 50px;
}

.testimonials-wrapper {
  position: relative;
  margin: auto;
  top: 15px;
  width: 90%;
  height: 90%;
  display: flex;
  gap: 40px;
}

.stacked-images {
  position: relative;
  width: 300px;
  height: 100%;
  perspective: 1000px;
}

.image-card {
  position: absolute;
  width: 100%;
  height: 100%;
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  transform-origin: center;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.image-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.image-card.behind {
  transform: translateX(-10%) scale(0.9);
  opacity: 0.7;
}

.image-card.active {
  transform: translateX(0) scale(1);
  opacity: 1;
  z-index: 3;
}

.image-card.front {
  transform: translateX(10%) scale(0.9);
  opacity: 0.7;
}

.text-content {
  flex: 1;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  padding: 20px;
}

.fixed-title {
  font-size: 24px;
  color: #ffffff;
  margin-bottom: 20px;
  display: flex;
  gap: 8px;
  z-index: 2;
}

.attribute {
  color: #66ccff;
  font-weight: bold;
  animation: fadeIn 0.3s ease-in-out;
}

.dynamic-content {
  position: absolute;
  width: 100%;
  top: 80px;
  opacity: 0;
  transform: translateX(50px);
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.dynamic-content.active {
  opacity: 1;
  transform: translateX(0);
}

.quote {
  font-size: 16px;
  color: #ffffff;
  line-height: 1.6;
  margin-bottom: 20px;
  font-style: italic;
  min-height: 80px;
}

.author-details {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.name {
  color: #66ccff;
  font-weight: bold;
  text-decoration: none;
  font-size: 18px;
  transition: color 0.3s ease;
}

.name:hover {
  color: #99ddff;
}

.designation {
  color: #999;
  font-size: 14px;
}

.navigation-arrows {
  position: absolute;
  bottom: 50px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 20px;
}

.arrow-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  background: rgb(40, 40, 40);
  color: gray;
  font-size: 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.arrow-btn:hover:not(:disabled) {
  background: rgba(102, 204, 255, 0.4);
  transform: scale(1.1);
}

.arrow-btn:active:not(:disabled) {
  transform: scale(0.95);
}

.arrow-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.image-card.behind {
  transform: translateX(-10%) translateY(2px) scale(0.9);
}

.image-card.front {
  transform: translateX(10%) translateY(2px) scale(0.9);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(5px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style> 