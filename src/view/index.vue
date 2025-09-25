<template>
  <div class="page">
    <img src="/island.png" alt="Logo" style="width: 100%; height: 100%" />
    <div
      v-for="(item, index) in POSITION"
      :key="index"
      :style="islandStyle(item)"
      @click="bigClick(item, index)"
    />
    <!-- <div class="da-chang-shan" @click="bigClick"></div>
    <div class="xiao-chang-shan"></div>
    <div class="guang-lu"></div>
    <div class="zhang-zi"></div>
    <div class="hai-yang"></div> -->
    <BigDialog ref="bigDialogRef"></BigDialog>
  </div>
</template>

<script setup>
// import { ElTooltip } from 'element-plus'
import BigDialog from './dialog.vue'
import { onMounted, ref } from 'vue'
// import { CONTENT } from '@/config/index.js'
import { POSITION } from '@/config/position'

const bigDialogRef = ref()
const configList = ref([])

onMounted(() => {
  init()
})

const init = async () => {
  fetch('https://raw.githubusercontent.com/tangwenbinaiduxue/sen-json/refs/heads/main/config.json')
    .then((res) => {
      console.log('Status:', res.status) // 应该是 200
      console.log('Headers:', res.headers)
      return res.text() // 先读取为文本
    })
    .then((text) => {
      console.log('Response Text:', text) // 查看真实内容
      try {
        const data = JSON.parse(text)
        configList.value = data
        console.log('Parsed JSON:', data)
      } catch (err) {
        console.error('JSON Parse Error:', err)
      }
    })
    .catch((err) => {
      console.error('Fetch Error:', err)
    })
}
const bigClick = (item, index) => {
  const content = configList.value[index] || ''
  bigDialogRef.value.show(item, content)
}

const islandStyle = (item) => {
  return {
    position: 'fixed',
    top: `${item.top}%`,
    left: `${item.left}%`,
    width: `${item.width}%`,
    height: `${item.height}%`,
    cursor: 'pointer',
  }
}
</script>

<style lang="scss" scoped>
.page {
  height: 100%;
  width: 100%;
}

.da-chang-shan {
  position: fixed;
  top: 9%;
  left: 22%;
  width: 18%;
  height: 12%;
  cursor: pointer;
  background: blue;
  opacity: 0.5;
}

.xiao-chang-shan {
  position: fixed;
  top: 24%;
  left: 36%;
  width: 16%;
  height: 12%;
  cursor: pointer;
  background: red;
  opacity: 0.5;
}

.guang-lu {
  position: fixed;
  top: 27%;
  left: 2%;
  width: 13%;
  height: 25%;
  cursor: pointer;
  background: rgb(48, 214, 15);
  opacity: 0.5;
}

.zhang-zi {
  position: fixed;
  top: 79%;
  left: 42%;
  width: 7%;
  height: 14%;
  cursor: pointer;
  background: rgb(8, 231, 231);
  opacity: 0.5;
}

.hai-yang {
  position: fixed;
  top: 67%;
  left: 88%;
  width: 7%;
  height: 20%;
  cursor: pointer;
  background: rgb(239, 243, 6);
  opacity: 0.5;
}
</style>
