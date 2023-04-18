<template>
  <div class="blog_detail">
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
    <div class="detail_contain">
      <div class="blog_detail_left">
        <div class="left_blog_info">
          <BlogInfo />
        </div>
        <div class="left_development_trend">
          <DevelopmentTrend />
        </div>
        <div class="left_essential_node">
          <EssentialNode />
        </div>
      </div>
      <div class="blog_detail_center">
        <PropagateTree />
      </div>
      <div class="blog_detail_right">
        <div class="right_cloud_graph">
          <CloudGraph />
        </div>
        <div class="right_topic_analysis">
          <TopicAnalysis />
        </div>
        <div class="right_hot_point">
          <HotPoint />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SideBorder from "../components/Side_border";
import BlogInfo from "../components/blog_detail/blog_info";
import CloudGraph from "../components/blog_detail/cloud_graph";
import DevelopmentTrend from "../components/blog_detail/development_trend";
import EssentialNode from "../components/blog_detail/essential_node";
import HotPoint from "../components/blog_detail/hot_point";
import PropagateTree from "../components/blog_detail/propagate_tree";
import TopicAnalysis from "../components/blog_detail/topic_analysis";
export default {
  name: "blog_detail",
  components: {
    SideBorder,
    BlogInfo,
    CloudGraph,
    DevelopmentTrend,
    EssentialNode,
    HotPoint,
    PropagateTree,
    TopicAnalysis,
  },
};
</script>

<style>
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
.blog_detail {
  width: 100%;
  display: flex;
  height: 100%;
  overflow:hidden;
  background-color: transparent;
}
.blog_detail_left,
.blog_detail_right {
  float: left;
  height: 100%;
  width: 30%;
  position: relative;
}
.side {
  width: 50px;
}
.detail_contain {
  background-color: transparent;
  width: 100%;
  height: 100%;
}
.blog_detail_center {
  position: relative;
  width: 37%;
  height: 100%;
  float: left;
  margin: 0 10px;
}
</style>