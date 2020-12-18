<template>
  <div :class="$style['ringContainer']" :style="'width: '+ringSize+'; height: '+ringSize+';'" >
    <svg viewBox="0 0 100 100" style="height: 100%; width: 100%" preserveAspectRatio="none">
       <circle :style="ringStyle" cx="50" cy="50" :r="innerRadius" fill="#456" />
    </svg>
  </div>
</template>

<script>
export default {
  props: ['current', 'max', 'innerText','size', 'color'],
  data(){
    return{
      ringWidth: 13
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
      result += 'transform: rotate(-90deg); transform-origin: 50% 50%; transition: 0.2s;'
      return result;
    },
  }
}
</script>

<style module lang="less">
.ringContainer{
  // background-color: blue;
  // display: flex;
  // align-items: center;
  // justify-content: center;
  margin: 3px;
  // border-radius: 50%;
  // box-sizing: border-box;
}

</style>
