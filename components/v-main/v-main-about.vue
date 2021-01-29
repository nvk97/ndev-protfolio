<template>
  <div class="about" v-show="visible">Обо мне</div>
</template>
<script>
export default {
  props: ["activeId"],
  computed: {
    visible: function () {
      return this.activeId == 2 ? true : false;
    },
  },
};
</script>