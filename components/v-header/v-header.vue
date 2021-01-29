<template>
  <header class="container">
    <div :class="$style.header">
      <vHeaderLogo :light="light"/>
      <div :class="$style.header_buttons">
        <vHeaderToggle :light="light"/>
        <vHeaderMenu :light="light"/>
      </div>
    </div>
  </header>
</template>

<script>
import vHeaderLogo from "@/components/v-header/v-header-logo";
import vHeaderToggle from "@/components/v-header/v-header-toggle";
import vHeaderMenu from "@/components/v-header/v-header-menu";
export default {
  head(){
    return{
      bodyAttrs: {
        class:this.light?"light":""
      }
    }
  },
  components: {
    vHeaderLogo,
    vHeaderToggle,
    vHeaderMenu,
  },
  data(){
    return{
      light:false
    }
  },
  created(){
    this.$nuxt.$on('toggle-mode',()=>{
      this.light= this.light?false:true
      this.light?document.body.classList.remove('light'):document.body.classList.add('light')
    })

    }
  
  
};
</script>

<style lang="scss" module>
.header {
  height:15vh;
  display: flex;
  align-items: center;
  justify-content: space-between;
  &_buttons {
    display: flex;
    align-items: center;
  }
}
</style>