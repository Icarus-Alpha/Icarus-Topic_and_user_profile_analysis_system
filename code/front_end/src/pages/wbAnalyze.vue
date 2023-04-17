<template>
  <div class="wbAnalyze">

    <css-doodle>
      
    </css-doodle>

    <div class="side">
      <SideBorder />
    </div>
    <div class="container">
      <div class="top">
        <Search />
      </div>
      <div class="main">
        <div class="left">
          <DefaultPanel />
        </div>
        <div class="center">
          <BlogHot />
          <TopicHot />
        </div>
        <div class="right">
          <div class="word">
            <WordCloud />
          </div>
          <div class="graph">
            <RelationGraph />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'css-doodle'
import SideBorder from "../components/Side_border";
import BlogHot from "../components/wbAnalyze/Blog_hot";
import DefaultPanel from "../components/wbAnalyze/Default_panel";
import RelationGraph from "../components/wbAnalyze/Relation_graph";
import Search from "../components/wbAnalyze/Search";
import TopicHot from "../components/wbAnalyze/Topic_hot";
import WordCloud from "../components/wbAnalyze/Word_cloud";

export default {
  name: "wbAnalyze",
  components: {
    BlogHot,
    DefaultPanel,
    RelationGraph,
    Search,
    TopicHot,
    WordCloud,
    SideBorder,
  },
};
</script>



<style scoped>
css-doodle {
  /* 将<css-doodle>元素定位在左上角 */
  height: 100%;
  margin: 0;
  overflow: hidden;
  display: flex;
  position: absolute;
  align-items: center;
  justify-content: center;
  /* 将<css-doodle>元素的 z-index 设置为 -1，使其在其他元素之下 */
  z-index: -1;
}

.wbAnalyze {
  background-color: rgb(106, 88, 88);
  z-index: 1;
  width: 100%;
  display: flex;
  height: 100%;
}

.side {
  width: 3.5%;
  z-index: 1;
  margin: 0;
}

.container {
  /* background-color: transparent; */

  width: 100%;
  height: 100%;
  margin: 0;
  overflow: hidden;
}

.top {
  height: 6%;
}

.main {
  margin: 10px 10px 0;
  height: 92%;
}

.left {
  height: 100%;
  width: 15%;
  float: left;
}

.center {
  height: 100%;
  float: left;
  width: 55%;
  margin: 0 0.5%;
  position: relative;
}

.right {
  height: 100%;
  width: 27.5%;
  float: left;
  position: relative;
}

.blog_hot {
  margin-bottom: 1%;
  height: 57%;
  width: 100%;
}

.topic_hot {
  width: 100%;
  height: 41.8%;
}
.word {
  width: 100%;
  margin-bottom: 10px;
}

.graph {
  width: 100%;
}
</style>