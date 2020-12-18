<template>
  <div :class="$style['ringContainer']" :style="'width: '+ringSize+'; height: '+ringSize+';'" >
    <div :class="$style['background']" ></div>

    <svg viewBox="0 0 100 100" style="height: 100%; width: 100%; position: absolute; " preserveAspectRatio="none">
       <circle :style="ringStyle" cx="50" cy="50" :r="innerRadius" fill="none" />
    </svg>

    <div :class="$style['ring-border']" ></div>
    <div :class="$style['center']" >
      <h3>{{innerText}}</h3>
    </div>
  </div>
</template>

<script>
export default {
  props: ['current', 'max', 'innerText','size', 'color'],
  data(){
    return{
      ringWidth: 12
    }
  },
  computed: {
    ringSize: function(){
      let result = "125px";
      if(typeof this.size !== "undefined"){
        result = this.size;
      }
      return result;
    },
    ringColor: function(){
      let result = "";
      if(typeof this.color !== "undefined"){
        result += this.color;
      }else{
        result += "yellow";
      }
      return (result);
    },
    innerRadius: function(){
      return 50-(this.ringWidth/2);
    },
    ringStyle: function(){
      let result = 'stroke: '+this.ringColor+'; stroke-width: '+this.ringWidth+';'
      let total = 2*Math.PI*this.innerRadius
      let curr = (this.current/100)*total
      result += 'stroke-dasharray: '+ curr + ' ' + (total-curr)+';';
      result += 'transform: rotate(-90deg); transform-origin: 50% 50%; transition: 0.15s;'

      return result;
    },
  }
}
</script>

<style module lang="less">
.ringContainer{
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 3px;

  .center{
    /*background-color: #666;
    border-radius: 50%;*/
    background-image: url(https://i.imgur.com/4CpEzjw.png);
    background-size: contain;
    position: absolute;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    box-sizing: border-box;
    //border: 5px solid rgba(0,0,0,0.05);
    >h3{
      color: black;
    }
  }
  .background{
    //background-color: #666;
    //border-radius: 50%;
    background-image: url(https://i.imgur.com/L0t0VGD.png);
    background-size: contain;
    position: absolute;
    width: 100%;
    height: 100%;
  }
}
.ring-border{
  width: 100%;
  height: 100%;
  position: absolute;
  box-sizing: border-box;
  background-image: url(https://i.imgur.com/zjIWXLV.png);
  background-size: contain;
}

</style>
