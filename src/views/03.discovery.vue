<template>
  <div class="discovery-container">
    <el-carousel class="" :interval="4000" type="card">
      <el-carousel-item v-for="(item, index) in banners" :key="index">
        <img :src="item.imageUrl" alt="" />
      </el-carousel-item>
    </el-carousel>
    <div class="recommend">
      <h3 class="title">
        推荐歌单
      </h3>
      <div class="items">
        <div class="item" v-for="item in playList" :key="item.id">
          <div class="img-wrap" @click="topPlayList(item.id)">
            <div class="desc-wrap">
              <span class="desc">{{ item.copywriter }}</span>
            </div>
            <img :src="item.picUrl" alt="" />
            <span class="iconfont icon-play"></span>
          </div>
          <p class="name">{{ item.name }}</p>
        </div>
      </div>
    </div>
 
    <div class="news">
      <h3 class="title">
        最新音乐
      </h3>
      <div class="items">
        <div class="item" v-for="(item, index) in newsong" :key="index">
          <div class="img-wrap">
            <img :src="item.picUrl" alt="" />
            <span @click="playMusic(item.id)" class="iconfont icon-play"></span>
          </div>
          <div class="song-wrap">
            <div class="song-name">{{ item.name }}</div>
            <div class="singer">{{ item.song.artists[0].name }}</div>
          </div>
        </div>
      </div>
    </div>
    <div class="mvs">
      <h3 class="title">推荐MV</h3>
      <div class="items">
        <div class="item" v-for="item in mv" :key="item.id">
          <div class="img-wrap" @click="toMv(item.id)">
            <img :src="item.picUrl" alt="" />
            <span class="iconfont icon-play"></span>
            <div class="num-wrap">
              <div class="iconfont icon-play"></div>
              <div class="num">{{ item.playCount }}</div>
            </div>
          </div>
          <div class="info-wrap">
            <div class="name">{{ item.copywriter }}</div>
            <div class="singer">{{ item.artistName }}</div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import {banner,songlist,newsong,mv,songUrl} from '@/api/discovery';
export default {
    name: 'discovery',
    data() {
      return {
        banners: [],
        playList: [],
        newsong: [],
        mv:[],
        songUrl:""
      }
    },
    created() {
     banner().then(res=>{
       this.banners=res.banners;
     })
     songlist().then(res=>{
       this.playList=res.result
     })
     newsong().then(res=>{
       this.newsong=res.result
     })
     mv().then(res=>{
       this.mv=res.result
     })
    },
    methods: {
      toMv(id){
        this.$router.push(`/mv?id=${id}`)
      },
      toPlayList(id){
        this.$router.push(`/playlist?id=${id}`)
      },
      playMusic(id){
        songUrl({
          id:id
        }).then(res=>{
          this.$parent.url=res.data[0].url
        })
      }
    }
}
</script>
<style lang='scss'>

</style>