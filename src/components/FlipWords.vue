<template>
  <span class="flip-words-wrapper">
    <span class="flip-word" :class="{ 'active': currentIndex === index }" v-for="(word, index) in words" :key="index">
      {{ word }}
    </span>
  </span>
</template>

<script>
export default {
  name: 'FlipWords',
  props: {
    words: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      currentIndex: 0
    }
  },
  mounted() {
    setInterval(this.flipWord, 2000)
  },
  methods: {
    flipWord() {
      this.currentIndex = (this.currentIndex + 1) % this.words.length
    }
  }
}
</script>

<style scoped>
.flip-words-wrapper {
  position: relative;
  display: inline-block;
  min-width: 120px;
  margin: 0 10px;
}

.flip-word {
  position: absolute;
  left: 0;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.5s ease;
  color: #66ccff;
  font-weight: bold;
}

.flip-word.active {
  opacity: 1;
  transform: translateY(0);
}
</style> 