<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon"></span>
          <span  class="text">{{seller.supports[0].description}}</span>
        </div>
        <div v-if="seller.supports" class="support-count" @click="showDetail">
          <span class="count">{{seller.supports.length}}个</span>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
    </div>
    <div class="backgroud">
      <img :src="seller.avatar" width="100%" height="100%" >
    </div>
    <transition name="fade">
    <div v-show="detailShow" class="detail" >
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <v-star></v-star>
          <div class="title1">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul v-if="seller.supports" class="supports">
            <li class="support-item" v-for="(item,index) in seller.supports">
              <span class="icon" :class="classMap[seller.supports[index].type]"></span>
              <span class="text">{{seller.supports[index].description}}</span>
            </li>
          </ul>
          <div class="title1">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="bulletin">
            <p class="content">{{seller.bulletin}}</p>
          </div>
        </div>
      </div>
      <div class="detail-close"  @click="hideDetail">×</div>
    </div>
    </transition>
  </div>
</template>
<script type="text/ecmascript-6">
 import star from '@/components/star/star';

export default{
  props:{
    seller:{
      type:Object
    }
  },
  data(){
    return {
      detailShow:false
    }
  },
   created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
  methods:{
    showDetail(){
      this.detailShow = true;
    },
    hideDetail(){
      this.detailShow = false;
    }
  },
  components:{
    'v-star':star
  }
}


</script>
<style>
  .header{
  color: #fff;
  width: 100%;
  background: rgba(7, 17, 27, 0.5);
    position: relative;
    overflow: hidden;
  }
  .fade-enter{
    opacity: 0;
  }
  .fade-enter-active{
    transition: all 0.5s;
    opacity: 1;
  }
  .fade-leave{
    opacity: 1;
  }
  .fade-leave-active{
    opacity: 0;
    transition: all 0.5s;
  }

  .content-wrapper{
  position: relative;
  padding: 24px 12px 18px 24px;
  font-size: 0;
  }
  .avatar{
  display: inline-block;
  vertical-align: top;
  }
  .avatar>img{
  border-radius: 2px;
  }
  .content{
  display: inline-block;
  margin-left: 16px;
  }
  .content .title{
      margin: 2px 0 8px 0;
   }
  .brand{
  display: inline-block;
  vertical-align: top;
  width: 30px ;
  height: 18px;
  background-size: 30px 18px;
  background-repeat: no-repeat;
  background-image: url("../../assets/img/brand@2x.png");
  }
   .name{
   margin-left: 6px;
    font-size: 16px;
    line-height: 18px;
    font-weight: bold;
   }
     .description{
     margin-bottom: 10px;
     line-height: 12px;
     font-size: 12px;
     }
     .support>.icon{
  display: inline-block;
  vertical-align: top;
  width: 12px;
  height: 12px;
  margin-right: 4px;
  background-size: 12px 12px;
  background-repeat: no-repeat;
  background-image: url("../../assets/img/decrease_1@3x.png");
  }
  .text{
  line-height: 12px;
  font-size: 10px;
  }
  .support-count{
    position: absolute;
    right: 12px;
    bottom: 18px;
    padding: 0 8px;
    height: 24px;
    line-height: 24px;
    border-radius: 14px;
    background: rgba(0,0,0,0.2);
    text-align: center;
  }
  .count{
    font-size: 10px;

  }
  .bulletin-wrapper{
    height: 28px;
    line-height: 28px;
    padding: 0 22px 0 12px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    background: rgba(7,17,27,0.2);
  }
  .bulletin-title{
    display: inline-block;
    width: 22px;
    height: 12px;
    background-image: url("../../assets/img/bulletin@3x.png");
    background-size: 22px 12px;
    background-repeat: no-repeat;
    vertical-align: top;
    margin-top: 8px;
  }
  .bulletin-text{
    font-size: 10px;
    margin: 0 4px ;
    vertical-align: top;
  }
  .backgroud{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    filter: blur(10px);
  }
  .detail{
    position: fixed;
    z-index: 100;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background: rgba(7,17,27,0.8);
    transition: all 0.5s;
  }


  .clearfix{
    display: inline-block;
  }
  .clearfix:after{
    display: block;
    content: '';
    height: 0;
    line-height: 0;
    clear: both;
    visibility: hidden;
  }
  .detail-wrapper{
    min-height: 100%;
    width: 100%;
  }
  .detail-main{
    margin-top: 64px;
    padding-bottom: 64px;
  }
  .detail-close{
    font-size: 32px;
    position: relative;
    width: 40px;
    height: 40px;
    margin: -64px auto 0 auto;
    clear: both;
  }
  .name{
    line-height: 16px;
    text-align: center;
    font-size: 16px;
    font-weight:700;
  }
  .title1{
    width: 80%;
    margin:28px auto 24px auto;
    display: flex;
  }
  .line{
    flex: 1;
    position: relative;
    top: -6px;
    border-bottom: 1px solid rgba(255,255,255,0.2);
  }
  .title1 .text{
    padding: 0 12px;
    font-size: 14px;
    font-weight: 700;
  }
  .supports{
    width: 80%;
    margin: 0 auto;
  }
  .support-item{
    padding: 0 12px;
    margin-bottom: 12px;
    font-size: 0;
  }
  .support-item:last-child{
    margin-bottom: 0;
  }
  .icon{
    display: inline-block;
    width: 16px;
    height: 16px;
    vertical-align: top;
    margin-right: 6px;
    background-size: 16px 16px;
    background-repeat: no-repeat;
  }
  .supports .text{
    line-height: 16px;
    font-size: 12px;
  }
  .bulletin{
  width: 80%;
  margin: 0 auto;
  }
  .bulletin .content{
    padding: 0 12px;
    line-height: 24px;
    font-size: 12px;
  }
</style>
