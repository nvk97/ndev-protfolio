<template>
  <div :class="[$style.menuBtn, { [$style.light]: light },{[$style.pending]:pending}]">
    <svg
      width="24"
      height="9"
      viewBox="0 0 24 9"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <rect width="24" height="2" rx="1" fill="#DCDCDC" />
      <rect y="7" width="24" height="2" rx="1" fill="#DCDCDC" />
    </svg>
  </div>
</template>
<script>
import gsap from "gsap";
export default {
  props: ["light"],
  data() {
    return {
      pending: true,
    };
  },
  methods: {
    fadeIn() {
      gsap.from(`.${this.$style.menuBtn}`, {
        x: 100,
        opacity: 0,
        duration: 0.6,
        ease: "easeInCubic",
      });
    },
  },
  mounted() {
    this.pending=false
    this.fadeIn();
  },
};
</script>

<style lang="scss" module>
.menuBtn {
  &.light {
    rect {
      fill: $font-color-l;
    }
  }
  &.pending{
    display: none;
  }
}
</style>