<template>
  <div class="person_list">
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
    <div class="participation_list">
      <ParticipationList />
    </div>
    <div class="participation_graph">
      <ParticipationGraph />
    </div>
  </div>
</template>

<script>
import ParticipationList from "../components/person_list/participation_list";
import ParticipationGraph from "../components/person_list/participation_graph";
import SideBorder from "../components/Side_border";
export default {
  name: "person_list",
  components: {
    ParticipationList,
    ParticipationGraph,
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
.person_list {
  display: flex;
  width: 100%;
  height: 100%;
  overflow:hidden;
  background-color: transparent;
}
.side{
    width: 50px;
}
.participation_graph {
  float: left;
  position: relative;
  width: 25%;
  height: 100%;
  margin-left: 0.5%;
}
.participation_graph {
  width: 71%;
}
</style>