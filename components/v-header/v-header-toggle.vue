<template>
  <div class="toggle-mode" :class='{pending:pending}'>
    <svg-icon
      name="todarkmode"
      width="24px"
      height="24px"
      v-if="light"
      @click="$nuxt.$emit('toggle-mode')"
    />
    <svg-icon
      name="tolightmode"
      v-if="!light"
      width="24px"
      height="24px"
      @click="$nuxt.$emit('toggle-mode')"
    />
  </div>
</template>

<script>
import gsap from 'gsap'
export default {
  props: ["light"],
  data(){
    return{
      pending:true
    }
  },
  methods: {
    fadeIn() {
      gsap.from(`.toggle-mode`, {
        y: -100,
        opacity: 0,
        duration: 0.6,
        ease: "easeInCubic",
      });
    },
  },
  mounted() {
    this.pending = false
    this.fadeIn();
  },
};
</script>


<style lang="scss" scoped>
.toggle-mode {
  cursor: pointer;
  width: 24px;
  height: 24px;
  margin-right: 60px;
  &.pending{
    display: none;
  }
  @include sm-tablets{
    margin-right: 30px;
  }
  @include sm-mobile{
    margin-right: 30px;
  }
  @include esm-mobile{
     margin-right: 20px;
  }
}
</style>