<template>
  <div>
    <input type="text" v-model="addNumber">
    <button @click="addAmrBtn">添加播放录音</button>
    <audio src="../assets/audio/mario.amr"></audio>
    <div v-for="(n,index) in amrList" :key="index">
      <button @click="play(n)">{{n._isPlaying? '暂停':'播放'}}{{index}}</button>
    </div>
  </div>
</template>

<script>
  let BAR = require('benz-amr-recorder')
  export default {
    name: "AmrRecorder",
    data() {
      return {
        addNumber: 0,
        amrList: []
      }
    },
    methods: {
      addAmrBtn() {
        [...Array(+this.addNumber)].forEach(() => {
          this.addAmr()
        })
      },
      addAmr() {
        let amrObj = new BAR()
        amrObj.initWithUrl('https://benzleung.github.io/benz-amr-recorder/res/mario.amr')
        console.log(amrObj)
        this.amrList.push(amrObj)
      },
      play(amrObj){
        console.log(amrObj)
        if(amrObj._isPlaying){
          amrObj.stop()
        } else {
          amrObj.play()
        }
      }
    },
    mounted() {
      [...Array(0)].forEach(() => {
        this.addAmr()
      })
    }
  }
</script>

<style scoped>

</style>
