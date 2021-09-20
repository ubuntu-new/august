<template>
  <div class='$i18n.locale'>
    <!-- <TopPanel v-if="isShowing" @clicked="onTopPanelClose"></TopPanel> -->
    <TopHeader></TopHeader>
    <Menubar></Menubar>
    <nuxt />
    <Footer></Footer>
    <SiteLoader  v-if="loading" />
    <BackToTop></BackToTop>
  </div>
</template>
<style scoped>
.en {
 .div {
    height: 200px;
  }
  
}

.ar {
 .$i18n.locale {
    height: 250px;
  }
  // all the style for ar lang
}
</style>
<script>
import TopPanel from './TopPanel';
import TopHeader from './TopHeader';
import Menubar from './Menubar';
import Footer from './Footer';
import BackToTop from './BackToTop';
import SiteLoader from './SiteLoder';
export default {
  components: {
    TopPanel, TopHeader, Menubar, Footer, BackToTop, SiteLoader
  },
  data() {
    return {
      loading: true,
      isShowing: true
    }
  },
  methods: {
    onTopPanelClose (value) {
      this.isShowing = value;
    }
  },
  watch: {
    '$route' (pathUrl){
      this.loading = true;
      setTimeout(() => { this.loading = false; }, 600);
    }
  },
  mounted(){
    setTimeout(() => { this.loading = false; }, 600);
  }
}
</script>