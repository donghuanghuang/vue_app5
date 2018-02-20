<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" >
        <span class="inner icon-ali-offline_fill"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-ali-addition_fill">

    </div>
  </div>
</template>
<script type="text/ecmascript-6">
export default{
  props: {
      food: {
        type: Object
      }
    },

}


</script>
<style>

  .cartcontrol{
    font-size: 0;
  }
  .cartcontrol .cart-decrease{
    display: inline-block;
    padding: 6px;
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
  .cartcontrol .cart-add{
    display: inline-block;
    padding: 6px;
    line-height: 24px;
    font-size: 24px;
    color: rgb(0, 160, 220);
  }
  .cartcontrol .cart-count{
    display: inline-block;
    vertical-align: top;
    width: 12px;
    padding-top: 6px;
    line-height: 24px;
    text-align: center;
    font-size: 10px;
    color: rgb(147, 153, 159);
  }

</style>
