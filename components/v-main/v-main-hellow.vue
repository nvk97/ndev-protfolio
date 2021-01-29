<template>
  <div class="hellow" v-show="visible">Привет, меня зовут Никита и я...</div>
</template>

<script>
export default {
  props: ["activeId"],
  computed: {
    visible: function () {
        
      return this.activeId == 1 ? true : false;
    },
  },
  watch:{
      visible:function(){

      }
  },
  methods:{
      slideIn(){

      }
  }
};
</script>

<style lang="scss" scoped>
.hellow {
  font-size: 50px;
  font-weight: 300;
  margin-top: -15vh;
  margin-right: -24px;
}
</style>