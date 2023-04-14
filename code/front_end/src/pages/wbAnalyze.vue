<template>
  <div class="wbAnalyze">

    <css-doodle>
      --color: #51eaea, #fffde1, #ff9d76, #FB3569;

      @grid: 30x1 / 100vw 100vh / #270f34;

      :container {
      perspective: 30vmin;
      --deg: @p(-180deg, 180deg);
      }

      :after, :before {
      content: '';
      background: @p(--color);
      @place: @r(100%) @r(100%);
      @size: @r(6px);
      @shape: heart;
      }

      @place: center;
      @size: 18vmin;

      box-shadow: @m2(0 0 50px @p(--color));
      background: @m100(
      radial-gradient(@p(--color) 50%, transparent 0)
      @r(-20%, 120%) @r(-20%, 100%) / 1px 1px
      no-repeat
      );

      will-change: transform, opacity;
      animation: scale-up 12s linear infinite;
      animation-delay: calc(-12s / @I * @i);

      @keyframes scale-up {
      0%, 95.01%, 100% {
      transform: translateZ(0) rotate(0);
      opacity: 0;
      }
      10% {
      opacity: 1;
      }
      95% {
      transform:
      translateZ(35vmin) rotateZ(var(--deg));
      }
      }
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
          <div class="blog_hot">
            <BlogHot />
          </div>
          <div class="topic_hot">
            <TopicHot />
          </div>
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
  /* 将<css-doodle>元素的z-index设置为-1，使其在其他元素之下 */
  z-index: -1;
}

.wbAnalyze {
  width: 100%;
  display: flex;
  height: 100%;
}

.side {
  width: 50px;
  z-index: 1;
  margin: 0;
  overflow: hidden;
}

.container {
  background-color: transparent;
  width: 100%;
  height: 100%;
  z-index: 1;
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
  margin: 0 10px;
  position: relative;
}

.right {
  height: 100%;
  width: 27.5%;
  float: left;
  position: relative;
}

.blog_hot {
  width: 100%;
  margin-bottom: 10px;
}

.topic_hot {
  width: 100%;
}

.word {
  width: 100%;
  margin-bottom: 10px;
}

.graph {
  width: 100%;
}
</style>