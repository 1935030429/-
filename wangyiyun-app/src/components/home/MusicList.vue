<template>
  <div class="musicList">
    <div class="musicItem">
      <div class="title">发现好歌单</div>
      <div class="more">查看更多</div>
    </div>
    <div class="musicContent">
      <van-swipe
        :loop="false"
        :width="150"
        class="myswiper"
        :show-indicators="false"
      >
        <van-swipe-item v-for="item in state.musicList" :key="item">
          <router-link :to="{path: '/itemMusic', query: {id: item.id}}">
          <img :src="item.picUrl" alt="" />
          <span class="playCount">
            <svg class="icon" aria-hidden="true">
              <use xlink:href="#icon-24gl-play"></use>
            </svg>
            {{changeCount(item.playCount)}}
          </span>
          <span class="name">{{item.name}}</span>
          </router-link>
        </van-swipe-item>
      </van-swipe>
    </div>
  </div>
</template>
<script>
import { getMusicList } from "@/request/api/home.js";
import {reactive, onMounted} from 'vue'
export default {
  //vue2语法
  // data() {
  //   return {
  //     musicList: [],
  //   };
  // },
  // methods: {
  //   async getGedan() {
  //     let res = await getMusicList();
  //     console.log(res);
  //     this.musicList = res.data.result;
  //   },
  //   changeCount:function(num){
  //       if(num>=100000000){
  //           return (num/100000000).toFixed(1)+'亿'
  //       }else if(num >= 10000000){
  //           return (num/10000000).toFixed(1)+'千万'
  //       }else if(num >= 10000){
  //           return (num/10000).toFixed(1)+'万'
  //       }
  //   }
  // },
  // mounted() {
  //   this.getGedan();
  // },
  //vue3写法
  setup(){
    const state = reactive({
      musicList: [],
    })
    function changeCount(num){
        if(num>=100000000){
            return (num/100000000).toFixed(1)+'亿'
        }else if(num >= 10000000){
            return (num/10000000).toFixed(1)+'千万'
        }else if(num >= 10000){
            return (num/10000).toFixed(1)+'万'
        }
    }
    onMounted(async()=>{
      let res = await getMusicList();
       console.log(res);
       state.musicList = res.data.result;
    })
    return {state, changeCount}
  }
};
</script>
<style lang="less" scoped>
.musicList {
  width: 100%;
  height: 5rem;
  padding: 0.2rem;
  .musicItem {
    width: 100%;
    height: 0.6rem;
    display: flex;
    justify-content: space-around;
    margin-bottom: 0.2rem;
    .title {
      font-size: 0.4rem;
      font-weight: 900;
    }
    .more {
      border: 1px solid #ccc;
      text-align: center;
      line-height: 0.6rem;
      padding: 0 0.2rem;
      border-radius: 0.4rem;
    }
  }
  .musicContent {
    width: 100%;
    height: 4rem;
    .myswiper {
      height: 100%;
      //padding: 0.2rem;
      display: flex;
      justify-content: space-around;
      align-items: center;
      img{
        width: 100%;
        height: 150px;
        border-radius: 0.3rem;
        padding: 0 0.06rem;
      }
      span.name{
        font-size: 16px;
      }
      span.playCount{
        font-size: 16px;
      }
      span{
        svg{
          height: .32rem;
        }
      }
    }
  }
}
</style>