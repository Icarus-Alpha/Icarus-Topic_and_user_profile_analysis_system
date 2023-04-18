<template>
  <div class="search">
    <input type="text" v-model="key_word" class="input" placeholder="搜索话题" size="50" />
    <div class="search_button">
      <button @click="search()" class="blog_btn">搜索</button>
    </div>
    <div class="searchResult" v-show="searchResult">
      <div class="title">
        有关{{ key_word }}的话题
        <button @click="add()">分析</button>
        <div class="close" @click="searchResult = false">
          <i class="el-icon-close"></i>
        </div>
      </div>
      <div class="result" v-for="result in results" :key="result.weibo_id">
        <div class="userinfo">
          <div class="userAvator">
            <img class="headimg" :src="result.head" alt="" />
          </div>
          <div class="user">
            <div class="username">{{ result.screen_name }}</div>
            <div class="other-info">{{ result.created_at }}</div>
          </div>
        </div>
        <div class="text">
          {{ result.text | snippet }}
        </div>
        <div class="msg">
          关注({{ result.attitudes_count }}),评论({{ result.comments_count }}),热度({{ result.hot_count }})
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "search",
  data() {
    return {
      key_word: "",
      searchResult: false,
      results: "",
    };
  },
  //定义过滤器超多20个字
  filters: {
    snippet(value) {
      if (value.length > 200) return value.slice(0, 200) + "...";
      return value;
    },
  },
  methods: {
    search() {
      // console.log(this.key_word);
      this.searchResult = true;
      this.$axios.get("search?tag=" + this.key_word + "&cursor=1").then((res) => {
        console.log(res)
        this.results = res.data.data.result;
      });
    },
    add() {
      this.$axios.get('add_task?tag=' + this.key_word).then((res) => {
        console.log(res)
      });
      this.$confirm('此操作将分析该话题, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
      }).then(() => {
        this.$axios.get('add_task?tag=' + this.key_word).then((res) => {
          console.log(res)
        });
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消分析'
        });
      });
    }
  },
};
</script>

<style scpoed>
.search {
  display: flex;
  height: 100%;
}

.key {
  display: flex;
}

.input {
  position: relative;
  top: 32%;
  margin: 0 10px;
  height: 15%;
  color: #8707ff;
  border: 2px solid #8707ff;
  border-radius: 30px;
  padding: 10px 20px;
  background: transparent;

}

.input:active {
  box-shadow: 2px 2px 15px #8707ff inset;
}

.key {
  width: 98%;
  height: 100%;
  margin: 5px 5px;
  outline: none;
  border: 0;
  font-size: 20px;
  letter-spacing: 1px;
}


.blog_btn {
  margin: 8px 30px 0 0;
  height: 95%;
  width: 90%;
}

.blog_btn {
  border: none;
  background-color: #8707ff;
  color: white;
  font-size: 1.15rem;
  font-weight: 500;
  padding: 0.5rem 1.2rem;
  border-radius: 0.5rem;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
  cursor: pointer;
  transform: translate(1) translate(0, 0);
  transition: transform 225ms, box-shadow 225ms;
}

.blog_btn:hover {
  transform: scale(1.05) translate(0, -0.15rem);
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.35);
}

.blog_btn:active {
  transform: scale(1) translate(0, 0.15rem);
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
}

.searchResult {
  position: absolute;
  width: 30%;
  height: 100vh;
  background-color: #fff;
  z-index: 99;
  overflow: auto;
  border-right: 10px solid #ccc;
  border-left: 10px solid #ccc;
}

.searchResult::-webkit-scrollbar {
  display: none;
}

.wbtitle {
  font-size: 35px;
  font-weight: 500;
  color: #89ffff;
  letter-spacing: 2px;
  background-color: transparent;
  border-radius: 10px;
  margin: 0;
  width:30%;
  z-index: 2;
  font-family: iconfont;
}

.userinfo {
  display: flex;
}

.userAvator {
  width: 70px;
  height: 70px;
  margin-right: 15px;
  margin-left: 20px;
}

.headimg {
  width: 70px;
  height: 70px;
  border-radius: 50%;
}

.username {
  color: #539ce5;
  margin-top: 15px;
  font: 20px Helvetica, Verdana, Arial, SimHei, SimSun-ExtB;
  margin-bottom: 5px;
}

.result {
  padding-top: 15px;
  height: 20vh;
  font-size: 18px;
  border-bottom: 5px solid #ccc;
  display: flex;
  flex-direction: column;
}

.other-info {
  color: #888788;
}

.result:hover {
  background: #ccc;
  box-shadow: #888 0 0 0;
  cursor: pointer;
}

.text {
  margin: 80px 0 0 80px;
  flex: 1;
}

.title {
  font-size: 25px;
  font-weight: 600;
  text-align: center;
  margin-bottom: 10px;
  border-bottom: 5px solid #ccc;
}

.close {
  font-size: 25px;
  height: 20px;
  color: #000;
  float: right;
}

.msg {
  margin-bottom: 10px;
  margin-left: 20px;
  color: #ccc;
}</style>