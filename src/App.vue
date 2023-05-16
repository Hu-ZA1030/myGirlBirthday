<!--
 * @Author: 胡子安 7608877+huzian@user.noreply.gitee.com
 * @Date: 2022-10-02 15:48:48
 * @LastEditors: 胡子安 7608877+huzian@user.noreply.gitee.com
 * @LastEditTime: 2023-05-15 23:40:59
 * @FilePath: \my_girl\src\App.vue
 * @Description: 
 * 
 * Copyright (c) 2022 by 胡子安 7608877+huzian@user.noreply.gitee.com, All Rights Reserved. 
-->
<template>
  <div id="app">
    <!-- <audio
      style="opacity: 0"
      id="cheerMusic"
      ref="music"
      preload="auto"
      loop="loop"
      :src="music"
    ></audio> -->
    <router-view></router-view>
  </div>
</template>

<script>
import '@/assets/css/app.css'
export default {
  name: 'app',
  data() {
    return {
      music: require('./assets/video/birthday.mp3')
    }
  },
  mounted() {
    // this.audioAutoPlay('cheerMusic')
  },
  methods: {
    /*
     * @param: 参数
     * @return: 返回值
     * @desc: 监听是否在播放，若没有则触发播放
     */
    /* 自动播放音乐 */
    audioAutoPlay(id) {
      let music = document.getElementById(id)
      music.play()
      let play = function () {
        music.play()
        document.removeEventListener('touchstart', play, false)
      }
      music.play()
      document.addEventListener(
        'WeixinJSBridgeReady',
        function () {
          play()
        },
        false
      )
      document.addEventListener(
        'YixinJSBridgeReady',
        function () {
          play()
        },
        false
      )
      document.addEventListener('touchstart', play, false)
    },
    onBridgeReady() {
      console.log(" WeixinJSBridge.call('hideOptionMenu')")
      WeixinJSBridge.call('hideOptionMenu')
    },
    WeixinJSBridgeReady() {
      if (typeof WeixinJSBridge === 'undefined') {
        console.log('WeixinJSBridge ==== undefined')
        if (document.addEventListener) {
          document.addEventListener(
            'WeixinJSBridgeReady',
            this.onBridgeReady,
            false
          )
        } else if (document.attachEvent) {
          document.attachEvent('WeixinJSBridgeReady', this.onBridgeReady)
          document.attachEvent('onWeixinJSBridgeReady', this.onBridgeReady)
        }
      } else {
        this.onBridgeReady()
      }
    }
  }
}
</script>

<style lang="less" scoped>
#app {
  overflow-x: hidden;
  background: #e2cfb8;
}
</style>
