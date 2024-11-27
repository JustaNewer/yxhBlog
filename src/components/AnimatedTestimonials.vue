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
        <div 
          v-for="(testimonial, index) in testimonials" 
          :key="index"
          class="text-section"
          :class="{ 'active': currentIndex === index }"
        >
          <p class="quote">"{{ testimonial.description }}"</p>
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
export default {
  name: 'AnimatedTestimonials',
  data() {
    return {
      currentIndex: 0,
      testimonials: [
        {
          description: 'An epic tale of honor and loyalty in the dying days of the outlaw age. Experience the story of Arthur Morgan in this acclaimed open-world adventure.',
          title: 'Red Dead Redemption 2',
          link: 'https://store.steampowered.com/app/1174180/Red_Dead_Redemption_2/',
          url: '/img/games/rdr.jpg'
        },
        {
          description: 'Journey through Norse realms with Kratos and Atreus in this emotional tale of father and son, featuring intense combat and stunning visuals.',
          title: 'God of War',
          link: 'https://www.playstation.com/en-sg/games/god-of-war-ragnarok/',
          url: '/img/games/gow.jpg'
        },
        {
          description: 'A gripping story of survival in a post-apocalyptic world. Follow Joel and Ellie\'s emotional journey across America.',
          title: 'The Last of Us',
          link: 'https://www.playstation.com/en-sg/games/the-last-of-us-part-i/',
          url: '/img/games/tlou.jpg'
        },
        {
          description: 'Master the art of shinobi combat in this challenging action game. Face deadly enemies in a dark, twisted take on 1500s Japan.',
          title: 'Sekiro',
          link: 'https://store.steampowered.com/app/814380/Sekiro_Shadows_Die_Twice__GOTY_Edition/',
          url: '/img/games/sekiro.png'
        },
        {
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
      }
    },
    getZIndex(index) {
      return this.testimonials.length - Math.abs(this.currentIndex - index)
    }
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
  width: 100%;
  height: 100%;
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
  transform-origin: center left;
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
  transform: translateX(-30%) scale(0.9);
  opacity: 0.7;
}

.image-card.active {
  transform: translateX(0) scale(1);
  opacity: 1;
}

.image-card.front {
  transform: translateX(30%) scale(0.9);
  opacity: 0.7;
}

.text-content {
  flex: 1;
  position: relative;
  overflow: hidden;
}

.text-section {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0;
  transform: translateX(50px);
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 20px;
}

.text-section.active {
  opacity: 1;
  transform: translateX(0);
}

.quote {
  font-size: 16px;
  color: #ffffff;
  line-height: 1.6;
  margin-bottom: 20px;
  font-style: italic;
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
  bottom: -40px;
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
  background: rgba(102, 204, 255, 0.2);
  color: #66ccff;
  font-size: 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.arrow-btn:hover {
  background: rgba(102, 204, 255, 0.4);
  transform: scale(1.1);
}

.arrow-btn:active {
  transform: scale(0.95);
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
</style> 