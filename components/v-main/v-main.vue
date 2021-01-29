<template>
  <main class="main">
    <vMainHellow  :activeId="activeId"/>
    <vMainAbout  :activeId="activeId"/>
    <vMainPortfolio :activeId="activeId"/>
  </main>
</template>

<script>
import vMainHellow from "@/components/v-main/v-main-hellow";
import vMainAbout from "@/components/v-main/v-main-about";
import vMainPortfolio from "@/components/v-main/v-main-portfolio";
export default {
  props: ["activeId"],
  components: {
    vMainHellow,
    vMainAbout,
    vMainPortfolio,
  },
};
</script>


<style lang="scss" scoped>
.main {
  height: 100%;
  width: calc(100% - 24px);
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
