<template>
  <div id="app">
    <el-container>
      <el-header>
        <basicHeader></basicHeader>
      </el-header>
      <el-main>
        <router-view></router-view>
      </el-main>
      <el-footer>
        <basicFooter></basicFooter>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
import basicHeader from "./components/basic/basicHeader.vue";
import basicFooter from "./components/basic/basicFooter.vue";
export default {
  name: "app",
  components: {
    basicHeader,
    basicFooter
  },
  created() {
    if (sessionStorage.getItem("store")) {
      this.$store.replaceState(
        Object.assign(
          {},
          this.$store.state,
          JSON.parse(sessionStorage.getItem("store"))
        )
      );
    }

    //在页面刷新时将vuex里的信息保存到sessionStorage里
    window.addEventListener("beforeunload", () => {
      sessionStorage.setItem("store", JSON.stringify(this.$store.state));
    });
  },
  mounted() {}
};
</script>

<style>
@import "./assets/css/normalize.css";
@import "./assets/css/ma.min.css";
@font-face {
  font-family: "iconfont"; /* project id 1481498 */
  src: url("//at.alicdn.com/t/font_1481498_ytrqu85r3p.eot");
  src: url("//at.alicdn.com/t/font_1481498_ytrqu85r3p.eot?#iefix")
      format("embedded-opentype"),
    url("//at.alicdn.com/t/font_1481498_ytrqu85r3p.woff2") format("woff2"),
    url("//at.alicdn.com/t/font_1481498_ytrqu85r3p.woff") format("woff"),
    url("//at.alicdn.com/t/font_1481498_ytrqu85r3p.ttf") format("truetype"),
    url("//at.alicdn.com/t/font_1481498_ytrqu85r3p.svg#iconfont") format("svg");
}
.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -webkit-text-stroke-width: 0.2px;
  -moz-osx-font-smoothing: grayscale;
}
#app {
  font-family: Helvetica, Helvetica Neue, "Avenir", Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
.el-main {
  padding: inherit !important;
  flex: 1 1;
}
.el-header {
  padding: inherit !important;
}
.el-footer {
  padding: inherit !important;
}
</style>
