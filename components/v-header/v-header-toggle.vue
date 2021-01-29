<template>
  <div class="toggle-mode">
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
export default {
  props:['light']
}
</script>


<style lang="scss" scoped>
.toggle-mode {
  cursor: pointer;
  width: 24px;
  height: 24px;
  margin-right: 60px;
}
</style>