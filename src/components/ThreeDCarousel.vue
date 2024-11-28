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
          @mouseleave="handleMouseLeave">
          <img :src="image.url" :alt="image.title" />
          <div class="image-overlay" v-show="hoveredIndex === index">
            <div class="title-container">
              <a :href="image.link" target="_blank" class="game-title-link">
                {{ image.title }}
                <span class="arrow">↗</span>
              </a>
            </div>
            <p class="game-description">{{ image.description }}</p>
          </div>
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
          {
            url: '/img/games/rdr.jpg',
            title: 'Red Dead Redemption 2',
            link: 'https://store.steampowered.com/app/1174180/Red_Dead_Redemption_2/',
            description: 'An epic tale of honor and loyalty in the dying days of the outlaw age. Experience the story of Arthur Morgan in this acclaimed open-world adventure.'
          },
          {
            url: '/img/games/gow.jpg',
            title: 'God of War',
            link: 'https://www.playstation.com/en-sg/games/god-of-war-ragnarok/',
            description: 'Journey through Norse realms with Kratos and Atreus in this emotional tale of father and son, featuring intense combat and stunning visuals.'
          },
          {
            url: '/img/games/tlou.jpg',
            title: 'The Last of Us',
            link: 'https://www.playstation.com/en-sg/games/the-last-of-us-part-i/',
            description: 'A gripping story of survival in a post-apocalyptic world. Follow Joel and Ellie\'s emotional journey across America.'
          },
          {
            url: '/img/games/sekiro.png',
            title: 'Sekiro',
            link: 'https://store.steampowered.com/app/814380/Sekiro_Shadows_Die_Twice__GOTY_Edition/',
            description: 'Master the art of shinobi combat in this challenging action game. Face deadly enemies in a dark, twisted take on 1500s Japan.'
          },
          {
            url: '/img/games/elden.png',
            title: 'Elden Ring',
            link: 'https://store.steampowered.com/app/1245620/Elden_Ring/',
            description: 'Rise, Tarnished, and explore a vast open world filled with epic battles, mysterious stories, and challenging dungeons.'
          },
          {
            url: '/img/games/hk.jpg',
            title: 'Hollow Knight',
            link: 'https://store.steampowered.com/app/367520/Hollow_Knight/',
            description: 'Explore a vast underground kingdom of insects and heroes in this beautiful, hand-drawn metroidvania adventure.'
          }
        ],
        rotationY: 0,
        hoveredIndex: null,
        autoSlideInterval: null
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
        this.stopAutoSlide()
      },
      handleMouseLeave() {
        this.hoveredIndex = null
        this.startAutoSlide()
      },
      nextSlide() {
        this.currentIndex = (this.currentIndex + 1) % this.images.length
        this.rotationY -= this.anglePerItem
      },
      prevSlide() {
        this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length
        this.rotationY += this.anglePerItem
      },
      startAutoSlide() {
        this.autoSlideInterval = setInterval(() => {
          this.nextSlide()
        }, 3000)
      },
      stopAutoSlide() {
        clearInterval(this.autoSlideInterval)
      }
    },
    mounted() {
      this.startAutoSlide()
    },
    beforeDestroy() {
      this.stopAutoSlide()
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
    overflow: hidden;
    border-radius: 10px;
  }
  
  .image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 10px;
    box-sizing: border-box;
    transition: all 0.3s ease;
    border-radius: 10px;
  }
  
  .image-title {
    color: white;
    font-size: 14px;
    margin: 0;
    text-align: left;
    font-weight: bold;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.8);
    max-width: 180px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
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
    left: 350px;
  }
  
  .next {
    right: 350px;
  }
  
  .carousel-item:hover img {
    filter: blur(2px);
  }
  
  .title-container {
    margin-bottom: auto;
  }
  
  .game-title-link {
    color: white;
    text-decoration: none;
    font-size: 14px;
    font-weight: bold;
    position: relative;
    display: inline-block;
    padding-right: 20px; /* 为箭头留出空间 */
    border-bottom: 1px dashed rgba(255, 255, 255, 0.7); /* 虚线 */
    max-width: 170px; /* 确保文字不会超出范围 */
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  
  .arrow {
    position: absolute;
    top: -2px;
    right: 0;
    font-size: 16px;
    line-height: 1;
  }
  
  .game-title-link:hover {
    color: #66ccff; /* 鼠标悬浮时改变颜色 */
    border-bottom-color: #66ccff;
  }
  
  .game-title-link:hover .arrow {
    color: #66ccff;
  }
  
  .game-description {
    color: #e0e0e0;
    font-size: 12px;
    line-height: 1.3;
    margin: 0 0 10px 0;
    text-align: left;
    max-height: 80px;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
  }
  </style> 