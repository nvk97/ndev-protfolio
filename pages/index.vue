<template>
  <div class="container" v-touch:swipe.top="swipeUp"  v-touch:swipe.down="swipeDown">
    <vMain :activeId="activeId" />
    <vNav :activeId="activeId" />
  </div>
</template>
<script>
import vNav from "@/components/v-nav/v-nav";
import vMain from "@/components/v-main/v-main";
export default {
  data() {
    let currentId = this.$nuxt.$route.hash;
    switch (currentId) {
      case "#hellow":
        currentId = 1;
        break;
      case "#about":
        currentId = 2;
        break;
      case "#portfolio":
        currentId = 3;
        break;
    }

    return {
      activeId: !!currentId ? currentId : 0,
      links: [
        {
          to: "#hellow",
          id: 1,
        },
        {
          to: "#about",
          id: 2,
        },
        {
          to: "#portfolio",
          id: 3,
        },
      ],
      disableScroll: false,
      disableRedirect: false,
    };
  },
  components: {
    vNav,
    vMain,
  },
  methods: {
    changeSlide(to) {
      
      this.activeId = to;
      this.$router.push(this.links[to - 1].to);
    },
    handleScroll(e) {
      if (!this.disableScroll) {
        this.disableScroll = true;
        setTimeout(() => (this.disableScroll = false), 1500);
        if ((e.deltaY > 0) & !(this.activeId == 3)) {
          let to = this.activeId;
          this.changeSlide(++to);
        } else {
          if ((e.deltaY < 0) & !(this.activeId == 1)) {
            let to = this.activeId;
            this.changeSlide(--to);
          }
        }
      }
    },
    swipeDown(){
      if (this.activeId != 1 && !this.disableRedirect){
        this.disableRedirect = true
        setTimeout(()=>this.disableRedirect=false,1500)
        let to = this.activeId
        to-=1
        this.changeSlide(to)
      }
    },
    swipeUp(){
      if (this.activeId != 3 && !this.disableRedirect){
        this.disableRedirect = true
        setTimeout(()=>this.disableRedirect=false,1500)
        let to = this.activeId
        to+=1
        this.changeSlide(to)
      }
    }
  },
  created() {
    this.$nuxt.$on("redirect", (id, to) => {
      if (!this.disableRedirect) {
        this.disableRedirect = true;
        setTimeout(() => (this.disableRedirect = false), 1500);
        this.changeSlide(id);
        this.$nuxt.$router.push(to);
      }
    });
  },
  mounted() {
    if (!!!this.$route.hash) {
      this.$nuxt.$emit("redirect", this.links[0].id, this.links[0].to);
    }
    document.body.addEventListener("wheel", this.handleScroll);
  },
  destroyed() {
    document.body.removeEventListener("wheel", this.handleScroll);
  },
};
</script>
<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 85vh;
}
</style>



