<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    
    <home-swiper :banners="banners"/>

    <recommend-view :recommends="recommends"/>

    <feature-view/>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper"
import RecommendView from "./childComps/RecommendView"
import FeatureView from "./childComps/FeatureView"
import { getHomeMultiData } from "network/home";
export default {
  data() {
    return {
      banners: [],
      recommends: [],
    };
  },
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
  },
  created() {
    getHomeMultiData().then((res) => {
      console.log(res);
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  },
};
</script>


<style>
#home {
  padding-top: 44px;
}
.home-nav {
  background-color: var(--color-text);
  color: white;

  position: fixed;
  top: 0;
  left: 0;
  right: 0;

  z-index: 9;

}
</style>