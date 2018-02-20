<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
   <div class="tab">
     <div class="tab-item">
       <router-link :class="{tab_a:true,response:true}" @click="showColor=!showColor" to="/goods">商品</router-link>
     </div>
     <div class="tab-item">
       <router-link :class="{tab_a:true,response:true}" to="/ratings">评论</router-link>
     </div>
     <div class="tab-item">
       <router-link :class="{tab_a:true,response:true}" to="/seller">商家</router-link>
     </div>
   </div>
    <keep-alive>
        <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header';
  const ERR_OK = 0;

export default {
  data() {
    return {
      seller:{},
      showColor : false,
    };
  },
  created() {
      this.$http.get('/api/seller?id=' + this.seller.id).then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = Object.assign({}, this.seller, response.data);
        }
      });
    },
  components:{
    'v-header':header
  }
};
</script>

<style>
  @import "common/font/iconfont.css";
    .tab{
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    }
  .response:hover{
    font-size: 15px;
    color: darkred;
    font-weight: bold;
  }
    .tab_a{
      text-decoration: none;
      display: block;
    font-size: 14px;
    color: rgb(77, 85, 93);
    }
   .tab-item{
   flex: 1;
   text-align: center;
   }

</style>
