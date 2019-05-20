<template>
  <div :class="$style['ringContainer']" :style="'width: '+ringSize+'; height: '+ringSize+';'">
    <div :class="$style['background']" ></div>
    <div :class="$style['ring']" :style="'clip-path:'+ mask +';'"></div>
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
      let result = "background-color: ";
      if(typeof this.color !== "undefined"){
        result += this.color;
      }else{
        result += "yellow";
      }
      return (result+";");
    },
    mask: function(){
      let result = "polygon(50% -50%, 50% 50%, ";
      let perc = 100*(this.current/this.max);
      let p = ((perc%25)/25);
      if(perc < 25){
        let x = (100*p)+50;
        let y = (100*p)-50;
        result += x+"% "+y+"%)";
      }else if(perc < 50){
        let x = 150-(100*p);
        let y = (100*p)+50;
        result += +x+"% "+y+"%, 150% 50%)";
      }else if(perc < 75){
        let x = 50-(100*p);
        let y = 150-(100*p);
        result += x+"% "+y+"%, 50% 150%, 150% 50%)";
      }else if(perc < 100){
        let x = (100*p)-50;
        let y = 50-(100*p);
        result += x+"% "+y+"%, -50% 50%, 50% 150%, 150% 50%)";
      }else{
        result = "";
      }
      return result;
    }
  }
}
</script>

<style module lang="less">
  .ring-border{
    width: 100%;
    height: 100%;
    position: absolute;
    box-sizing: border-box;
    background-image: url(https://i.imgur.com/zjIWXLV.png);
    background-size: contain;
  }
  .ringContainer{
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 3px;
    .ring{
      width: 100%;
      height: 100%;
      position: absolute;
      box-sizing: border-box;
      //border-radius: 50%;
      background-image: url(https://i.imgur.com/y67bqFC.png);
      background-size: contain;
      //border: 5px solid rgba(0,0,0,0.2);
    }
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
</style>
