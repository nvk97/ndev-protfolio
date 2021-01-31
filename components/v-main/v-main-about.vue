<template>
  <div class="about" v-show="visible">
    <div class="about-description">
      <div class="about-description__title">Frontend <br/>Developer</div>
      <div class="about-description__subtitle">
        <span>Разрабатываю</span> интерфейсы и сайты с помощью:<br />
        HTML5<br />
        CSS(SCSS)<br />JS(ES6+)<br />
        Vue.JS/Nuxt.js<br />
        <span>Живу</span> в Москве <br /><span>Мечтаю</span> работать в команде
      </div>
    </div>
    <VMainAboutLaptop />
  </div>
</template>
<script>
import gsap from "gsap";
import vMainAboutLaptop from "@/components/v-main/v-main-about-laptop";
export default {
  props: ["activeId"],
  components: {
    vMainAboutLaptop,
  },
  data() {
    return {
      visible: false,
    };
  },
  watch: {
    activeId: function (newId, oldId) {
      if (newId == 2) {
        if ((!oldId == 1) && (!oldId == 3)) {
          this.slideIn(400);
        } else if(oldId==1){
          this.slideIn(400);
        }else if(oldId==3){
          this.slideIn(1500);
        }
      } else if (newId != 2) {
        this.slideOut(1000);
      }
    },
  },
  methods: {
    handleChange() {},
    slideIn(del) {
      setTimeout(() => {
        this.visible = true
        let tl = gsap.timeline()
        tl.fromTo('.about-description__title',{duration:0.3,opacity:0,y:-20,ease:'easeInCubic'},{opacity:1,y:0})
        .fromTo('.about-description__subtitle',{duration:0.3,opacity:0,x:-20,ease:'easeInCubic'},{opacity:1,x:0})
        this.$nuxt.$emit('laptopFadeIn')

      },del)
    },
    slideOut(del) {
       let tl = gsap.timeline()
       this.$nuxt.$emit('laptopFadeOut')
        tl.to('.about-description__subtitle',{duration:0.3,opacity:0,x:20,ease:'easeInCubic',delay:0.4})
        .to('.about-description__title',{duration:0.3,opacity:0,y:20,ease:'easeInCubic'})
      setTimeout(() => (this.visible = false), del);
    },
  },
  created() {
    if (this.$nuxt.$route.hash == "#about") {
      this.slideIn(800);
    }
  },
};
</script>


<style lang="scss" scoped>
.about {
  display: flex;
  width: 100%;
  height: 100%;
  &-description {
    width: 35%;
    &__title {
      margin-top: 50px;
      font-weight: bold;
      font-size: 62px;
    }
    &__subtitle {
      margin-top: 20px;
      font-weight: 300;
      font-size: 26px;
      span{
        font-weight:bold;
      }
    }
  }
  @include md-desktop{
    
  }
  @include sm-tablets{
    &-description{
      &__title {
        margin-top: 0;
        font-size: 40px;
      }
      &__subtitle {
        font-size: 20px;
      }
    }
  }
  @include sm-mobile{
    flex-direction: column;
    align-items: center;
    &-description{
      width: 100%;
      &__title {
        margin-top: 0;
        font-size: 50px;
      }
      &__subtitle {
        font-size: 20px;
      }
    }
  }
  @include esm-mobile{
    flex-direction: column;
    align-items: center;
    &-description{
      width: 100%;
      &__title {
        margin-top: 0;
        font-size: 35px;
      }
      &__subtitle {
        font-size: 18px;
      }
    }
  }
}
</style>