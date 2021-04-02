<template>
  <div id="app">
    <div class="header">
      <img src="./assets/flower.png" title="送你一朵小红花，奖励你人生第一次积极主动~"/>
      <h2>任务计划列表</h2>
      <!-- <span class="cur-time">{{cur_time}}</span> -->
      <span class="punch-time">{{ clock | FormatTime }}</span>
    </div>
    <div id="nav">
      <!-- <router-link to="/"></router-link> -->
      <router-view />
    </div>
  </div>
</template>

<script>
import { getDate } from './common/format.js'
export default {
  name: 'app',
  data () {
    return {
      clock: Date.parse(new Date())
    }
  },
  // computed() {
  //   cur_time() {

  //   }
  // },
  mounted () {
    const _this = this
    setInterval(function () {
      _this.clock = Date.parse(new Date())
    }, 1000)
  },
  filters: {
    FormatTime: function (val) {
      return getDate(val, 'hour')
    }
  }
}
</script>

<style lang="scss">
body, html {
  height: 100%;
  overflow: hidden;
}
.cur-time {
  position: absolute;
  left: 0;
  color: #fff;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  height: 100%;
}

#nav {
  height: 100%;
  flex: 1;
  position: relative;
  /* padding: 30px; */
  /* background: url("./assets/bg.png"); */
  /* background-size: contain; */
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.header {
  width: 100%;
  height: 80px;
  color: #fff;
  line-height: 80px;
  text-align: center;
  background-color: #879ac1;
  position: relative;
  h2 {
    font-size: 30px;
    letter-spacing: 6px;
  }
  img {
    width: 50px;
    height: 50px;
    position: absolute;
    top: 50%;
    left: 38%;
    transform: translateY(-50%);
    animation:turn 4s linear infinite;
    cursor: pointer;
    &:hover {
      animation: unset;
    }
  }
}
.punch-time {
  position: absolute;
  right: 10px;
  top: 0px;
  font-size: 22px;
  letter-spacing: 2px;
  color: #ffebeb;
}
/*
  turn : 定义的动画名称
  1s : 动画时间
  linear : 动画以何种运行轨迹完成一个周期
  infinite :规定动画应该无限次播放
  */
@keyframes turn{
  0%{
    -webkit-transform: translateY(-50%) rotate(0deg);
  }
  25%{
    -webkit-transform: translateY(-50%) rotate(90deg);
  }
  50%{
    -webkit-transform: translateY(-50%) rotate(180deg);
  }
  75%{
    -webkit-transform: translateY(-50%) rotate(270deg);
  }
  100%{
    -webkit-transform: translateY(-50%) rotate(360deg);
  }
}
#app::-webkit-scrollbar{

  width: 8px;
  height: 8px;
  &::horizontal{
    height: 10px;
  }
}
#app::-webkit-scrollbar-button {
  &:end, &:start {
    &:increment, &:decrement{
      background-color: #dcdee2;
      border-radius: 4px;
      display: none;
      &:hover {
        background-color: #999;
      }
    }
  }
}
#app::-webkit-scrollbar-thumb {
  background-color: #dcdee2;
  border-radius: 4px;
  &:hover {
    background-color: #999;
  }
}
#app::-webkit-scrollbar-track-piece {
  background-color: #f8f8f9;
  border-radius: 4px;
}
</style>
