<template>
  <div class="vue-cobra" :style="{ ...styles, width: this.getProgress }"></div>
</template>

<script>
export default {
  name: "vueCobra",
  data() {
    return {
      progress: 0,
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
    }
  },
  computed: {
    getProgress() {
      return this.progress + "%";
    }
  },
  methods: {
    GetPercentageScroll(scrollPosition) {
      const bodyHeight =
        document.body.clientHeight - document.documentElement.clientHeight;
      return Math.floor((scrollPosition / bodyHeight) * 100);
    },
    SetProgress() {
      this.progress = this.GetPercentageScroll(window.scrollY);
    }
  },
  created() {
    this.styles = {
      height: this.height + "px",
      "background-color": this.color,
      opacity: this.opacity,
      "z-index": this.zIndex
    };
  },
  mounted() {
    window.addEventListener("scroll", () => {
      this.SetProgress();
    });
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
  background-color #4fc08d
</style>
