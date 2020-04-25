eal<template>
  <div
    class="vue-cobra"
    :style="{
      ...styles,
      transform: getProgressTransform,
      ...this.getStylesOnCustomPosition
    }"
  />
</template>

<script>
export default {
  name: "vueCobra",
  data() {
    return {
      progress: 0,
      ticking: false,
      styles: {}
    };
  },
  props: {
    height: {
      type: Number,
      default: 4
    },
    color: {
      type: String,
      default: "#000"
    },
    opacity: {
      type: Number,
      default: 1
    },
    zIndex: {
      type: Number,
      default: 1000
    },
    position: {
      type: String,
      default: "top",
      validator(value) {
        return ["left", "bottom", "top"].indexOf(value) !== -1;
      }
    }
  },
  computed: {
    getProgressTransform() {
      if (this.position === "left" || this.position === "right") {
        return `scaleY(${this.progress / 100})`;
      } else {
        return `scaleX(${this.progress / 100})`;
      }
    },
    getStylesOnCustomPosition() {
      switch (this.position) {
        case "left":
          return {
            height: "100%",
            width: `${this.height}px`,
            "transform-origin": "top",
            left: 0
          };
        case "bottom":
          return {
            top: "initial",
            bottom: 0
          };
        default:
          return {};
      }
    }
  },
  methods: {
    getPercentageScroll() {
      const scrollPosition = window.pageYOffset;
      const bodyHeight =
        document.body.clientHeight - document.documentElement.clientHeight;
      return Math.floor((scrollPosition / bodyHeight) * 100);
    },
    setProgress() {
      if (this.ticking === false) {
        window.requestAnimationFrame(() => {
          this.progress = this.getPercentageScroll();
          this.ticking = false;
        });

        this.ticking = true;
      }
    }
  },
  created() {
    this.styles = {
      height: `${this.height}px`,
      "background-color": this.color,
      opacity: this.opacity,
      "z-index": this.zIndex,
      top: 0,
      left: 0,
      position: "fixed"
    };
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.setProgress);
  },
  mounted() {
    window.addEventListener("scroll", this.setProgress);
  }
};
</script>

<style lang="stylus" scoped>
.vue-cobra
  top 0
  left 0
  width 100%
  height 4px
  position fixed
  transform-origin left
</style>
