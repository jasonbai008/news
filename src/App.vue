<template>
  <div id="app">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="百度热搜" name="0"></el-tab-pane>
      <el-tab-pane label="抖音热榜" name="1"></el-tab-pane>
      <el-tab-pane label="哔哩哔哩" name="6"></el-tab-pane>
      <el-tab-pane label="知乎" name="2"></el-tab-pane>
      <el-tab-pane label="头条" name="4"></el-tab-pane>
      <el-tab-pane label="微博" name="3"></el-tab-pane>
      <el-tab-pane label="36氪" name="5"></el-tab-pane>
      <el-tab-pane label="IT资讯" name="7"></el-tab-pane>
    </el-tabs>
    <div class="bot-wrap" v-loading="loading" element-loading-text="拼命加载中">
      <list :listData="listData" :updateDate="updateDate" ref="newsList" />
    </div>
  </div>
</template>

<script>
import list from "@/components/List.vue";

export default {
  name: "App",
  components: {
    list,
  },
  data() {
    return {
      loading: false,
      activeName: localStorage.tabNum ? localStorage.tabNum : "0",
      type: ["baiduRD", "douyinHot", "zhihuHot", "wbHot", "toutiao", "36Ke", "bili", "itNews"],
      listData: [],
      updateDate: "",
    };
  },
  mounted() {
    this.handleClick({ name: this.activeName });
  },
  methods: {
    handleClick(tab) {
      this.loading = true;
      this.$refs.newsList.$el.scrollTo(0, 0);
      localStorage.tabNum = tab.name; // 缓存标签位置
      let i = Number(tab.name);
      fetch(`https://api.vvhan.com/api/hotlist/${this.type[i]}`)
        .then((response) => response.json())
        .then((data) => {
          this.listData = data.data;
          this.updateDate = data.update_time;
          this.loading = false;
        });
    },
  },
};
</script>

<style lang="scss">
body {
  height: 100vh;
  margin: 0;
  overflow: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 90%;
  max-width: 640px;
  margin: 1vh auto 2vh;
  height: 97vh;
}
.el-tabs__item.is-active {
  font-weight: bold;
}
</style>
