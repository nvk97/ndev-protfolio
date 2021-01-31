<template>
  <div class="portfolio" v-show="visible">
    <div class="projects">
      <vMainPortfolioCase
        v-for="project in projects"
        :key="project.id"
        :project="project"
        :light="light"
      />
    </div>
    <vMainPortfolioCaseInfo />
  </div>
</template>

<script>
import vMainPortfolioCase from "@/components/v-main/v-main-portfolio-case";
import vMainPortfolioCaseInfo from '@/components/v-main/v-main-portfolio-case-info'
import anime from 'animejs'
export default {
  props: ["activeId"],
  components: {
    vMainPortfolioCase,
    vMainPortfolioCaseInfo
  },
  data() {
    return {
      visible: false,
      light:false,
      projects: [
        {
          name: "NDEV",
          to: "/",
          descr: "Личное портфолио(NUXT,HTML5,SCSS,GSAP+ANIME.JS)",
          id: 1,
          icon:'ndev',
          iconL:'ndevl'
        },
        {
          name: "SimpleEng",
          to: "http://javascriptizer.ru/game",
          descr:
            "Приложение(MEVN)",
          id: 2,
          icon:'SimpleEng',
          iconL:'SimpleEngl'
        },
        {
          name: "GitHub",
          to: "https://github.com/nvk97",
          descr:
            "Мой GitHub",
          id: 3,
          icon:'GitHub',
          iconL:'GitHubl'
        },
      ],
    };
  },
  watch: {
    activeId: function (newId, oldId) {
      if (newId == 3) {
        if ((!oldId == 2) && (!oldId == 1)) {
          this.slideIn(0);
        } else {
          this.slideIn(1500);
        }
      } else if (newId != 3) {
        this.slideOut();
      }
    },
  },
  methods: {
    handleChange() {},
    slideIn(del) {
      setTimeout(() => (this.visible = true), del);
      anime({
        targets:'.project',
        opacity:[0,1],
        translateX:[50,0],
        easing:"easeInCubic",
        duration:300,
        delay:anime.stagger(200,{start:del+10})
      })
    },
    slideOut() {
       anime({
        targets:'.project',
        opacity:[1,0],
        translateX:[0,-50],
        easing:"easeOutCubic",
        duration:300,
        delay:anime.stagger(200,{start:100})
      })
      setTimeout(() => (this.visible = false), 1450);
    },
  },
  created() {
    if (this.$nuxt.$route.hash == "#portfolio") {
      this.slideIn(0);
    }
    this.$nuxt.$on('toggle-mode',()=>{
      this.light= this.light?false:true
    })
  },
};
</script>

<style lang="scss" scoped>
.portfolio {
  width: 100%;
  height: 100%;
  margin-top: -15vh;
  margin-right: -24px;
  .projects {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    row-gap: 50px;
    column-gap: 50px;
  }
  @include sm-tablets{
    margin-right: 0;
    margin-top: -20px;
    .projects {
      flex-direction: column;
      row-gap:20px;
    column-gap: 20px;
    }
  }
  @include sm-mobile{
    margin-right: 0;
    margin-top: -20px;
    .projects {
      flex-direction: column;
        row-gap:20px;
    column-gap: 20px;
    }
  }
  @include esm-mobile{
    margin-right: 0;
     margin-top: -20px;
    .projects {
      flex-direction: column;
        row-gap:20px;
    column-gap: 20px;
    }
  }
}
</style>