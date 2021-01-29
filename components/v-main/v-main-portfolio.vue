<template>
  <div class="portfolio" v-show="visible">Портфолио</div>
</template>

<script>
export default {
  props: ["activeId"],
  computed: {
    visible: function () {
      return this.activeId == 3 ? true : false;
    },
  },
};
</script>