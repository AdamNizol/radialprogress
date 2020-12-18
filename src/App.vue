<template>
  <div id="app">
    <progress-radial :current="health" :max="maxHealth"  size="80px" color="yellow" :innerText="health"></progress-radial>
    <progress-ring :current="health" :max="maxHealth"  size="80px" color="#938d76" :innerText="health"></progress-ring>
    <input type="range" min="0" max="100" v-model="health"></input>
  </div>
</template>

<script>
import ProgressRadial from './components/ProgressRadial.vue'
import ProgressRing from './components/ProgressRing.vue'

export default {
  name: 'app',
  components: {
    'progress-radial':ProgressRadial,
    'progress-ring':ProgressRing,
  },
  data(){
    return{
      health: 20,
      maxHealth: 100,
      characterLevel: 5
    }
  }
}
</script>

<style lang="less">
body {
  margin: 0;
}
#app{
  >input[type=range]::-webkit-slider-runnable-track {
      width: 100%;
      height: 14px;
      cursor: pointer;
      box-shadow: 1px 1px 5px #000000, 0px 0px 1px #0d0d0d;
      background: #444a59;
      border-radius: 1.3px;
      border: 1px solid #010101;
    }
    >input[type=range] {
      margin: 3px;
      -webkit-appearance: none;
      width: 125px;
    }
    > input[type=range]::-webkit-slider-thumb {
      box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
      border: 1.5px solid #00000c;
      height: 14px;
      width: 26px;
      border-radius: 4px;
      background: #7d808b;
      cursor: pointer;
      -webkit-appearance: none;
      margin-top: -1px;
    }
}
</style>
