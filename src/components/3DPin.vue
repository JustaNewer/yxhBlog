<template>
  <div class="pin-container">
    <div 
      class="pin-content"
      :class="{ 'hover': isHovered }"
      @mouseenter="isHovered = true"
      @mouseleave="isHovered = false"
    >
      <a 
        v-if="href" 
        :href="href" 
        class="pin-link"
        target="_blank"
      >
        <div class="link-line"></div>
        <span class="link-text">{{ title }}</span>
      </a>
      <div class="pin-inner">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: '3DPin',
  props: {
    title: {
      type: String,
      default: ''
    },
    href: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      isHovered: false
    }
  }
}
</script>

<style scoped>
.pin-container {
  perspective: 1000px;
  width: 100%;
  height: 100%;
}

.pin-content {
  width: 100%;
  height: 100%;
  background: rgba(30, 30, 30, 0.8);
  border-radius: 20px;
  padding: 20px;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(0deg);
  transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

.pin-content.hover {
  transform: rotateX(40deg);
}

.pin-inner {
  width: 100%;
  height: 100%;
}

.pin-link {
  position: absolute;
  left: 50%;
  top: -60px;
  transform: translateX(-50%);
  color: #66ccff;
  text-decoration: none;
  opacity: 0;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
  z-index: 10;
}

.link-line {
  width: 2px;
  height: 30px;
  background: #66ccff;
  margin-bottom: 8px;
}

.link-text {
  padding: 4px 12px;
  background: rgba(0, 0, 0, 0.8);
  border-radius: 15px;
  font-size: 14px;
  white-space: nowrap;
}

.pin-content.hover .pin-link {
  opacity: 1;
}
</style> 