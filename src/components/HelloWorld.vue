<template>
  <div class="position-absolute-center text-center">
    <!-- 測試滾動才發現播放動畫 -->
    <!-- <div style="margin-bottom:2000px;"></div> -->
    <CountUp ref="countupRef"
             v-bind="property"
             class="text-30"
             @init="init"
             @finished="finished">
      <!-- 前贅字 -->
      <template #prefix>
        <span class="text-14 me-2" :style="textFixSlot['prefix'].style">
          {{ textFixSlot['prefix'].vModel }}
        </span>
      </template>
      <!-- 後贅字 -->
      <template #suffix>
        <span class="text-14 ms-2" :style="textFixSlot['suffix'].style">
          {{ textFixSlot['suffix'].vModel }}
        </span>
      </template>
    </CountUp>

    <!-- 設定區塊 -->
    <div class="my-15">
      <!-- 前、後贅字 -->
      <div v-for="item in textFixSlot" :key="item.enName">
        <div class="d-flex align-items-center">
          <!-- 設定文字 -->
          <div class="form-floating mb-3 me-2">
            <input type="text"
                   class="form-control"
                   :id="item.enName"
                   :placeholder="item.cnName"
                   v-model="textFixSlot[item.enName].vModel">
            <label :for="item.enName">{{ item.cnName }}(文字)</label>
          </div>
          <!-- 設定樣式 -->
          <div class="form-floating mb-3">
            <input type="text"
                   class="form-control"
                   :id="item.enName"
                   :placeholder="item.cnName"
                   v-model="textFixSlot[item.enName].style">
            <label :for="item.enName">{{ item.cnName }}(樣式)</label>
          </div>
        </div>
      </div>

      <!-- 屬性 -->
      <div v-for="item in setupProperty" :key="item.enName">
        <div class="form-floating mb-3">
          <input :type="item.type"
                 class="form-control"
                 :id="item.enName"
                 :placeholder="item.cnName"
                 v-model="property[item.enName]">
          <label :for="item.enName">{{ item.cnName }}</label>
        </div>
      </div>
    </div>

    <div class="d-flex align-items-center justify-content-center">
      <p class="text-20 me-5">{{ isPlaying?'播放中':'暫停中' }}</p>
      <button type='button'
              class='btn btn-primary me-5'
              @click="countupRef.init()"
              :disabled="isPlaying">
        初始化播放(包含延遲播放時間)
      </button>
      <button type='button'
              class='btn btn-primary'
              @click="countupRef.restart()"
              :disabled="isPlaying">
        重新播放
      </button>
    </div>
  </div>
</template>

<script setup>
import CountUp from 'vue-countup-v3'
import { ref } from 'vue'

const countupRef = ref(null)
const isPlaying = ref(false)
const textFixSlot = ref({
  prefix: { // 前贅字
    cnName: '前贅字',
    enName: 'prefix',
    vModel: '總共有',
    style: ['color:red;']
  },
  suffix: { // 後贅字
    cnName: '後贅字',
    enName: 'suffix',
    vModel: '個人造訪你的網站',
    style: ['color:blue;']
  }
})
const property = ref({
  endVal: String(Math.random() * 10).split('.').join(''), // 结束值
  startVal: 0, // 起始值
  duration: 5, // 動畫時間(秒)
  decimalPlaces: 0, // 小數點位數
  // autoplay: false, // 是否自動開始
  loop: false, // 重複次數(布林、數字)
  delay: 2, // 循環的間隔時間(秒)
  options: {
    useGrouping: true, // 是否開啟千分位
    separator: ',', // 千分位使用的符號
    decimal: '.',
    enableScrollSpy: true, // 在可視範圍內才開始動畫
    scrollSpyDelay: 2000 // 目標進入可視範圍後的延遲播放時間 (毫秒)
    // formattingFn: function (n) { // 格式化
    // return `${n}測試XD`
    // }
  }
})

// 用來迴圈跑出設定區塊的資料
const setupProperty = ref({
  endVal: {
    enName: 'endVal',
    cnName: '结束值',
    type: 'number'
  },
  startVal: {
    enName: 'startVal',
    cnName: '起始值',
    type: 'number'
  },
  duration: {
    enName: 'duration',
    cnName: '動畫時間(秒)',
    type: 'number'
  },
  decimalPlaces: {
    enName: 'decimalPlaces',
    cnName: '小數點位數',
    type: 'number'
  },
  loop: {
    enName: 'loop',
    cnName: '重複次數(布林、數字)',
    type: 'text'
  },
  delay: {
    enName: 'delay',
    cnName: '循環的間隔時間(秒)',
    type: 'number'
  }
})

// Countup 實體初始化完成後觸發
function init (e) {
  console.log('Countup 初始化完畢', e)
  if (!e.paused) isPlaying.value = true
}
// 倒數計時結束後觸發
function finished () {
  console.log('播放完畢')
  isPlaying.value = false
}
</script>

<style lang='scss' scope></style>
