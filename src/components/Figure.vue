<template>
    <div class="figure-container">
      <div v-show="showFigure" 
           :style="figureStyle" 
           :class="{ 'rounded': isRounded }">
        <p v-show="showText" :style="textStyle">{{ text }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Figure',
    props: {
      width: Number,
      height: Number,
      radius: Number,
      rotation: Number,
      color: String,
      textColor: String,
      text: String,
      font: String,
      fontSize: String,
      showFigure: Boolean,
      showText: Boolean
    },
    computed: {
      figureStyle() {
        return {
          width: this.width + 'px',
          height: this.height + 'px',
          backgroundColor: this.color,
          borderRadius: this.radius + 'px',
          transform: `rotate(${this.rotation}deg)`,
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center'
        }
      },
      textStyle() {
        return {
          color: this.textColor,
          fontFamily: this.font,
          fontSize: this.getFontSize(),
          margin: 0
        }
      },
      isRounded() {
        return this.radius > 0
      }
    },
    methods: {
      getFontSize() {
        switch(this.fontSize) {
          case 'small':
            return '12px';
          case 'medium':
            return '16px';
          case 'large':
            return '24px';
          default:
            return '16px';
        }
      }
    },
    watch: {
      color: {
        handler(newColor) {
          this.$emit('color-used', newColor)
        },
        immediate: true
      },
      textColor: {
        handler(newColor) {
          this.$emit('color-used', newColor)
        },
        immediate: true
      }
    }
  }
  </script>
  
  <style scoped>
  .figure-container {
    width: 45%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .rounded {
    border-radius: 50%;
  }
  </style>