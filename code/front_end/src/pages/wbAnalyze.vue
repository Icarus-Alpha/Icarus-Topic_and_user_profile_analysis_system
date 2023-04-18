<template>
  <div class="wbAnalyze">
    <css-doodle>
      :doodle {
      @grid: 1x3 / 100vmax;
      position: absolute;
      top: 0; left: 0;
      z-index: 0;
      }

      @size: 100% 150%;
      position: absolute;

      background: @m(100, (
      linear-gradient(transparent, @p(
      #FFFDE1@repeat(2, @p([0-9a-f])),
      #FB3569@repeat(2, @p([0-9a-f]))
      ))
      @r(0%, 100%) @r(0%, 100%) /
      @r(1px) @r(23vmin)
      no-repeat
      ));

      will-change: transform;
      animation: f 20s linear calc(-20s / @size() * @i()) infinite;
      @keyframes f {
      from { transform: translateY(-100%) }
      to { transform: translateY(100%) }
      }
    </css-doodle>

    <div class="side">
      <SideBorder />
    </div>
    <div class="container">
      <div class="top">
        <Search />
        <div class="head_top head_top_right">
          <img class="img-responsive" src="../assets/img/ksh32.png">
        </div>
        <div class="wbtitle">微博舆情分析</div>
        <div class="head_top">
          <img class="img-responsive" src="../assets/img/ksh31.png">
        </div>
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
  background-color: #061436;
}

.head_top {
  position: relative;
}

.head_top img {
  width: 80%;
  margin: 2% 0;
}

.head_top p {
  width: 100%;
  text-align: center;
  color: #55bfff;
  position: absolute;
  bottom: -18px;
  left: -10px;
}

.head_top p span {
  font-family: 'yjsz';
  font-size: 20px;
}
.head_top_right{
  margin-left: 1%;
}

.wbAnalyze {
  background-color: transparent;
  z-index: 1;
  width: 100%;
  display: flex;
  height: 100%;
}
.visual_conBot_l{position:absolute;left:0;top:0;}
.visual_conBot_2{position:absolute;right:0;top:0;}
.visual_conBot_3{position:absolute;right:0;bottom:0;}
.visual_conBot_4{position:absolute;left:0;bottom:0;}

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
  width: 100%;
  height: 6%;
  display: flex;
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
}</style>