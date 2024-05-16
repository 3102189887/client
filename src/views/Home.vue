<template>
  <div>
    <h2>欢迎使用教务管理(课程管理)系统</h2>
<h2><a href="http://www.java1234.com/a/bysj/javaweb/" target='_blank'><font color=red>Java1234收藏整理</font></a></h2>

    <el-col :span="16">
      <div class="fater-welcome-panel"></div>
    </el-col>
  </div>
</template>

<script>
// import * as api from "../api/news";

export default {
  name: "Home",
  data() {
    return {
      tableData: [],
    };
  },
  // methods: {
  //   query() {
  //     api.get().then(res => {
  //       this.tableData = res;
  //     });
  //   },
  //   openNews(url) {
  //     window.open(url, "_blank");
  //   }
  // },
  created() {
    this.query();
  },
};
</script>

<style scoped>
.fater-welcome-panel {
  height: 350px;
  width: 400px;
  margin-left: 400px;
  margin-bottom: 15px;
  border-radius: 5px;
  background-image: url("../assets/12.png");
  background-size: cover;
}
.home-wrap {
  height: 100%;
  width: 100%;
}

.main-wrap {
  margin-top: 10px;
  height: 100%;
  width: 100%;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.home-container {
  height: 100%;
  width: 90%;
  margin: auto;
}

.home-aside {
  height: 100%;
}

.aside-container {
  width: 90%;
  margin-left: auto;
  margin-right: auto;
  height: 200px;
  margin-top: 20px;
}

.aside-img {
  width: 100%;
}

.aside-title {
  color: #333;
  font-size: 18px;
}

.aside-content {
  font-size: 12px;
  color: #999;
}
</style>
