<template>
  <div :class="$style['ringContainer']">
    <div :class="$style['background']" ></div>
    <div :class="$style['ring']" :style="'clip-path:'+ mask +';'"></div>
    <div :class="$style['center']" >
      <h3>{{innerText}}</h3>
    </div>
  </div>
</template>

<script>
export default {
  props: ['current', 'max', 'innerText'],
  data(){
    return{

    }
  },
  computed: {
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
  .ringContainer{
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 150px;
    height: 150px;
    margin: 3px;
    .ring{
      background-color: rgb(220,220,0);
      width: 90%;
      height: 90%;
      border-radius: 50%;
      position: absolute;
      box-sizing: border-box;
      border: 5px solid rgba(0,0,0,0.2)
    }
    .center{
      background-color: #666;
      position: absolute;
      width: 75%;
      height: 75%;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      box-sizing: border-box;
      border: 5px solid rgba(0,0,0,0.05)
    }
    .background{
      background-color: #666;
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 50%;
    }
  }
</style>
