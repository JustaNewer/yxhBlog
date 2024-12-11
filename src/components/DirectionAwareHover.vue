<template>
  <div 
    class="direction-aware-container" 
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
    ref="container"
  >
    <img 
      :src="imageUrl" 
      :alt="alt" 
      class="hover-image"
      :style="imageStyle"
    >
    <div 
      class="content-overlay"
      :class="{ 'visible': isHovered }"
    >
      <div class="content-wrapper">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DirectionAwareHover',
  props: {
    imageUrl: {
      type: String,
      required: true
    },
    alt: {
      type: String,
      default: 'Hover image'
    }
  },
  data() {
    return {
      imageStyle: {
        transform: 'translate(-5%, -5%)',
        transition: 'transform 0.3s ease'
      },
      isHovered: false
    }
  },
  methods: {
    handleMouseEnter(e) {
      this.isHovered = true;
      const rect = this.$refs.container.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      
      // Calculate direction
      const dx = x - rect.width / 2;
      const dy = y - rect.height / 2;
      
      let angle = Math.atan2(dy, dx) * (180 / Math.PI);
      let direction;
      
      // Determine the direction based on angle
      if (angle >= -45 && angle < 45) direction = 'right';
      else if (angle >= 45 && angle < 135) direction = 'bottom';
      else if (angle >= -135 && angle < -45) direction = 'top';
      else direction = 'left';
      
      // Set image transform based on direction
      let imageTransform = '';
      switch(direction) {
        case 'left': imageTransform = 'translate(calc(-5% - 10px), -5%)'; break;
        case 'right': imageTransform = 'translate(calc(-5% + 10px), -5%)'; break;
        case 'top': imageTransform = 'translate(-5%, calc(-5% - 10px))'; break;
        case 'bottom': imageTransform = 'translate(-5%, calc(-5% + 10px))'; break;
      }
      
      this.imageStyle = {
        transform: imageTransform,
        transition: 'transform 0.3s ease'
      };
    },
    handleMouseLeave() {
      this.isHovered = false;
      this.imageStyle = {
        transform: 'translate(-5%, -5%)',
        transition: 'transform 0.3s ease'
      };
    }
  }
}
</script>

<style scoped>
.direction-aware-container {
  position: relative;
  width: 400px;
  height: 400px;
  overflow: hidden;
  border-radius: 1rem;
  cursor: pointer;
}

.hover-image {
  width: 110%;
  height: 110%;
  object-fit: cover;
  transform: translate(-5%, -5%);
}

.content-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 2rem;
  text-align: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
}

.content-overlay.visible {
  opacity: 1;
}

.content-wrapper {
  transform: translateY(0);
  transition: transform 0.3s ease;
}
</style> 