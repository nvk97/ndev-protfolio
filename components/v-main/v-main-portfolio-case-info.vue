<template>
  <div class="info">
    <div class="info-title">{{ title }}</div>
    <div class="info-description">{{ description }}</div>
  </div>
</template>

<script>
import anime from "animejs";
export default {
  data() {
    return {
      title: "",
      description: "",
      animateIn: {},
      animateOut: {},
    };
  },
  methods: {
    show() {
      this.animateIn.restart();
    },
    hide() {
      this.animateOut.restart();
    },
  },
  created() {
    this.$nuxt.$on("show-info", (title, description) => {
      this.title = title;
      this.description = description;
      this.show();
    });
    this.$nuxt.$on("hide-info", () => {
      this.hide();
    });
  },
  beforeMount() {
    this.animateOut = anime.timeline({ easing: "easeInCubic" }).add({
      targets: ".info",
      zIndex: {
        value: [20, -1],
        round: true,
      },
      opacity: [1, 0],
      duration: 500,
    });
    this.animateOut.pause();
    this.animateIn = anime
      .timeline({ easing: "easeInCubic" })
      .add({
        targets: ".info",
        zIndex: {
          value: [-1, 20],
          round: true,
        },
        opacity: [0, 1],
        duration: 500,
      })
      .add({
        targets: ".info-title",
        opacity: [0, 1],
        duration: 200,
        translateY: [-50, 0],
      })
      .add(
        {
          targets: ".info-description",
          opacity: [0, 1],
          duration: 200,
          translateY: [20, 0],
        },
        "-=100"
      );
    this.animateIn.pause();
  },
};
</script>

<style lang="scss" scoped>
.info {
  position: absolute;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: flex-start;
  padding-top: 15vh;
  background: rgba(27, 26, 26, 0.62);
  backdrop-filter: blur(5px);
  z-index: -1;
  user-select: none;
  &-title {
    margin-top: 50px;
    font-weight: bold;
    font-size: 72px;
    line-height: 100%;
    color: #dcdcdc;
  }
  &-description {
    margin-top: 10px;
    line-height: 100%;
    color: #dcdcdc;
  }
  @include lg-desktop {
    &-title {
      margin-top: 20px;
    }
    &-description {
    }
  }
  @include md-desktop {
    &-title {
      margin-top: 20px;
    }
    &-description {
    }
  }
  @include sm-tablets {
    display: none;
  }
  @include sm-mobile {
    display: none;
  }
  @include esm-mobile {
    display: none;
  }
}
</style>