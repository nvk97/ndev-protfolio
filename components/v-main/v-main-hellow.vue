<template>
  <div class="hellow" v-show="visible">Привет, меня зовут Никита и я...</div>
</template>

<script>
import gsap from "gsap";
export default {
  props: ["activeId"],
  data() {
    return {
      visible: false,
    };
  },
  watch: {
    activeId: function (newId, oldId) {
      if (newId == 1) {
        if (oldId == 0) {
          this.slideIn(300);
        } else if (oldId == 2) {
          this.slideIn(1100);
        } else if (oldId == 3) {
           this.slideIn(1500);
        }
      } else if (newId != 1) {
        this.slideOut(350);
      }
    },
  },
  methods: {
    handleChange() {},
    slideIn(del) {
      setTimeout(() => {
        this.visible = true;
        gsap.fromTo(
          ".hellow",
          { opacity: 0, y: -50 },
          { opacity: 1, y: 0, duration: 0.3, ease: "easeInCubic" }
        );
      }, del);
    },
    slideOut(del) {
      gsap.fromTo(
        ".hellow",
        { opacity: 1, y: 0 },
        { opacity: 0, y: 50, duration: 0.3, ease: "easeInCubic" }
      );
      setTimeout(() => (this.visible = false), del);
    },
  },
  mounted() {
    if (this.$nuxt.$route.hash == "#hellow") {
      this.slideIn(300);
    }
  },
};
</script>

<style lang="scss" scoped>
.hellow {
  font-size: 50px;
  font-weight: 300;
  margin-top: -15vh;
  margin-right: -24px;
  @include sm-tablets{
    font-size: 30px;
    margin-right: 0;
  }
  @include sm-mobile{
    font-size: 25px;
    margin-right: 0;
  }
  @include esm-mobile{
    font-size: 18px;
    margin-right: 0;
  }
}
</style>