<template>

  <div class="project" :class='{light:light}' @mouseenter="$nuxt.$emit('show-info',project.name,project.descr)" @mouseleave="$nuxt.$emit('hide-info')" @click="redirect">
      <svg-icon class='icon' v-if="!light" :name="project.icon" height="75px" width="200px"/>
      <svg-icon class='icon' v-if="light" :name="project.iconL" height="75px" width="200px"/>
  </div>
</template>

<script>
export default {
  props: ["project","light"],
  methods:{
    redirect(){
      window.location.href = `${this.project.to}`;
    }
  }
};
</script>

<style lang="scss" scoped>
.project {
  cursor: pointer;
  width: 250px;
  height: 250px;
  background: #ffffff;
  border-radius: 20px;
  row-gap: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition:0.3s;
  z-index: 5;
  &.light{
    background:#4F4F4F
  }
  &:hover{
    z-index: 25;
  }
  @include sm-tablets{
    width: 200px;
    height: 200px;
    .icon{
      height: 50px;
      width: 150px;
    }
  }
  @include sm-mobile{
    width:175px;
    height: 175px;
    .icon{
      height: 50px;
      width: 130px;
    }
  }
  @include esm-mobile{
     width:175px;
    height: 175px;
    .icon{
      height: 50px;
      width: 130px;
    }
  }
}
</style>