<template>
  <div class="position-absolute-center text-center">
    <CountUp v-bind="property" class="text-20">
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
  </div>
</template>

<script setup>
import CountUp from 'vue-countup-v3'
import { ref } from 'vue'

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
    vModel: '多個人造訪你的網站',
    style: ['color:blue;']
  }
})
const property = ref({
  endVal: '123456789', // 结束值
  startVal: 0, // 起始值
  duration: 5, // 動畫時間(秒)
  decimalPlaces: 2, // 小數點位數
  // autoplay: false, // 是否自動開始
  loop: true, // 重複次數(布林、數字)
  delay: 2, // 循環的間隔時間(秒)
  options: {
    // CountUp 套件的其他選項
    separator: ',',
    decimal: '.'
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

// let countUp = null // eslint-disable-line
// const onInit = (ctx) => {
//   console.log('init', ctx)
//   countUp = ctx
// }
// const onFinished = () => {
//   console.log('finished')
// }
</script>

<style lang='scss' scope></style>
