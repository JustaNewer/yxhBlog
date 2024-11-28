<template>
  <span class="typing-text">{{ displayText }}</span>
</template>

<script>
export default {
  name: 'TypingAnimation',
  props: {
    text: {
      type: String,
      required: true
    },
    typingSpeed: {
      type: Number,
      default: 25
    }
  },
  data() {
    return {
      displayText: '',
      currentIndex: 0
    }
  },
  watch: {
    text: {
      immediate: true,
      handler(newText) {
        this.startTyping(newText)
      }
    }
  },
  methods: {
    startTyping(text) {
      this.displayText = ''
      this.currentIndex = 0
      
      const typeNextChar = () => {
        if (this.currentIndex < text.length) {
          this.displayText += text[this.currentIndex]
          this.currentIndex++
          setTimeout(typeNextChar, this.typingSpeed)
        }
      }
      
      typeNextChar()
    }
  }
}
</script>

<style scoped>
.typing-text {
  border-right: 2px solid #66ccff;
  animation: blink 0.7s step-end infinite;
  white-space: pre-wrap;
}

@keyframes blink {
  from, to { border-color: transparent }
  50% { border-color: #66ccff }
}
</style> 