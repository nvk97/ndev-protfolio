<template>
  <div
    class="nav-link"
    :class="[{ active: activeId == link.id }, { light: light }]"
		@click="$nuxt.$emit('redirect',link.id,link.to)"
  >
    <div class="nav-link__descr">{{ link.descr }}</div>
    <div class="nav-link__circle"></div>
  </div>
</template>

<script>
export default {
  props: ["link", "activeId", "light"],
};
</script>
<style lang="scss" scoped>
.nav-link {
  cursor: pointer;
  height: 24px;
  display: flex;
  justify-content: center;
  &__descr {
    user-select: none;
    width: 0;
    height: 0;
    position: relative;
    top: -5px;
    right: 15px;
    white-space: nowrap;
    display: flex;
    justify-content: flex-end;
    opacity: 0;
    transition: opacity 0.1s;
    font-weight: 500;
  }
  &__circle {
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: $font-color;
    opacity: 0.3;
    transition: opacity 0.1s;
  }
  &:nth-child(2) {
    margin: 16px 0;
  }
  &.active {
    pointer-events: none;
    .nav-link__circle {
      opacity: 1;
    }
  }
  &:hover {
    .nav-link {
      &__circle {
        opacity: 1;
      }
      &__descr {
        opacity: 1;
      }
    }
  }
  &.light {
    .nav-link {
      &__circle {
        background: $font-color-l;
      }
    }
  }
}
</style>

