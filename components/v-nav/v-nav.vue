<template>
  <nav class="nav" :class="{pending:pending}">
    <vNavLink
      v-for="link in links"
      :key="link.to"
      :link="link"
      :light="light"
      :activeId="activeId"
    />
  </nav>
</template>


<script>
import vNavLink from "@/components/v-nav/v-nav-link";
import gsap from 'gsap'
export default {
  props:['activeId'],
  data() {
    return {
      links: [
        {
          descr: "Главная",
          to: "#hellow",
          id: 1,
        },
        {
          descr: "Обо мне",
          to: "#about",
          id: 2,
        },
        {
          descr: "Портфолио",
          to: "#portfolio",
          id: 3,
        },
      ],
      light: false,
      pending:true
    };
  },
  components: {
    vNavLink,
  },
  methods:{
    fadeIn(){
      gsap.from('.nav',{x:100,opacity:0,duration:0.6,ease:'easeInOutCubic'})
    }
  },
  created() {
    this.$nuxt.$on("toggle-mode", () => {
      this.light = this.light ? false : true;
    });
  },
  mounted(){
    this.pending = false
    this.fadeIn()
  },
  beforeDestroy() {
    this.$nuxt.$off("toggle-mode");
  },
};
</script>

<style lang="scss" scoped>
.nav {
  margin-top: -12vh;
  width: 24px;
  &.pending{
    display: none;
  }
  @include sm-tablets{
    display: none;
  }
  @include sm-mobile{
    display: none;
  }
  @include esm-mobile{
    display: none;
  }
}
</style>