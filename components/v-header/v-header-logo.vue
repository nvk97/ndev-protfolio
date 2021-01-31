<template>
    <NuxtLink to="/" :class="[$style.logo,{[$style.light]:light},{[$style.pending]:pending}]">
        <svg
          width="50"
          height="50"
          viewBox="0 0 75 75"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          id="logo"
        >
          <g>
            <path
              d="M67.1 75H74.2V1.20001H0.300003V75H49.1L44.7 68.1L7.1 67.9V7.90001H67.2L67.1 75Z"
              fill="#DCDCDC"
            />
            <path
              d="M67.2 75L72.7 70.5L51.2 43.1H42.4L67.2 75Z"
              fill="#DCDCDC"
            />
            <path d="M42.3 75H49.4V43.1H42.5L42.3 75Z" fill="#DCDCDC" />
          </g>
        </svg>
    </NuxtLink>
</template>

<script>
import gsap from 'gsap'
export default {
    props:['light'],
    data(){
    return{
      pending:true
    }
  },
    methods:{
      fadeIn(){
        gsap.from(`.${this.$style.logo}`,{x:-100,opacity:0,duration:0.6,ease:'easeInCubic'})
      }
    },
    mounted(){
      this.pending = false
      this.fadeIn()
    }
}
</script>

<style lang="scss" module>
    .logo{
        &.light{
            path{
                fill:$font-color-l
            }
        }
        &.pending{
          display: none;
        }
  @include sm-tablets{
    svg{
      width:50px;
      height:50px;
    }
  }
  @include sm-mobile{
    svg{
      width:30px;
      height:30px;
    }
  }
  @include esm-mobile{
    svg{
      width:30px;
      height:30px;
    }
  }
    }
</style>