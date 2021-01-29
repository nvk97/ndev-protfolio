<template>
  <div>
    <vHeader/>
    <Nuxt />
  </div>
</template>

<script>
import vHeader from '@/components/v-header/v-header'
import vNav from '@/components/v-nav/v-nav'
export default {
  components:{
    vHeader,
    vNav
  }
}
</script>
