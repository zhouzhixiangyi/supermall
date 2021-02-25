<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>

    <home-swiper :banners="banners" />

    <recommend-view :recommends="recommends" />

    <feature-view />

    <tab-control
      :titles="['流行', '新款', '精选']"
      class="tab-control"
    ></tab-control>

    <div style="height: 1000px"></div>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/tabControl/TabControl";

import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import FeatureView from "./childComps/FeatureView";

import { getHomeMultiData, getHomeGoods } from "network/home";
export default {
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sells: { page: 0, list: [] },
      },
    };
  },
  components: {
    NavBar,
    TabControl,
    HomeSwiper,
    RecommendView,
    FeatureView,
  },
  created() {
    this.getHomeMultiData();

  },
  methods: {
    // 获取导航数据
    getHomeMultiData() {
      getHomeMultiData().then((res) => {
        //console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    // 获取首页商品数据
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then((res) => {
        console.log(res);
        this.goods[type].list.push(...res.data.list)
        this.goods[page].page = page
      });
    },
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
.tab-control {
  position: sticky;
  top: 44px;
}
</style>