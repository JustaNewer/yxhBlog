<template>
  <div class="dots-container" ref="dotsContainer">
    <div v-for="dot in dots" 
         :key="dot.id" 
         class="dot"
         :style="getDotStyle(dot)">
    </div>
  </div>
</template>

<script>
export default {
  name: 'FloatingDots',
  props: {
    quantity: {
      type: Number,
      default: 100
    },
    ease: {
      type: Number,
      default: 80
    },
    color: {
      type: String,
      default: '#ffffff'
    }
  },
  data() {
    return {
      dots: [],
      mouseX: 0,
      mouseY: 0,
      containerRect: null
    }
  },
  mounted() {
    this.containerRect = this.$refs.dotsContainer.getBoundingClientRect()
    this.createDots()
    window.addEventListener('mousemove', this.handleMouseMove)
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy() {
    window.removeEventListener('mousemove', this.handleMouseMove)
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    createDots() {
      this.dots = Array.from({ length: this.quantity }, (_, i) => ({
        id: i,
        x: Math.random() * 100,
        y: Math.random() * 100,
        size: Math.random() * 2 + 1,
        originalX: Math.random() * 100,
        originalY: Math.random() * 100,
        speed: Math.random() * 0.02 + 0.01
      }))
    },
    handleMouseMove(e) {
      const rect = this.$refs.dotsContainer.getBoundingClientRect()
      this.mouseX = ((e.clientX - rect.left) / rect.width) * 100
      this.mouseY = ((e.clientY - rect.top) / rect.height) * 100
      
      this.dots = this.dots.map(dot => {
        const dx = this.mouseX - dot.x
        const dy = this.mouseY - dot.y
        const distance = Math.sqrt(dx * dx + dy * dy)
        
        // 只有在一定范围内的点才会受到影响
        if (distance < 20) {
          const force = (20 - distance) / 20
          dot.x += (dx * force * dot.speed)
          dot.y += (dy * force * dot.speed)
        } else {
          // 缓慢返回原始位置
          dot.x += (dot.originalX - dot.x) * 0.05
          dot.y += (dot.originalY - dot.y) * 0.05
        }
        
        return dot
      })
    },
    handleResize() {
      this.containerRect = this.$refs.dotsContainer.getBoundingClientRect()
    },
    getDotStyle(dot) {
      return {
        position: 'absolute',
        left: `${dot.x}%`,
        top: `${dot.y}%`,
        width: `${dot.size}px`,
        height: `${dot.size}px`,
        backgroundColor: this.color,
        borderRadius: '50%',
        opacity: 0.2,
        transition: `all ${this.ease}ms cubic-bezier(0.175, 0.885, 0.32, 1.275)`
      }
    }
  }
}
</script>

<style scoped>
.dots-container {
  position: absolute;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
}

.dot {
  position: absolute;
  will-change: transform;
}
</style>