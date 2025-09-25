<template>
  <el-dialog
    v-model="visible"
    :title="title"
    :close-on-click-modal="false"
    :lock-scroll="false"
    :style="{ height: '50%' }"
  >
    <div v-for="(item, index) in text" :key="index" style="white-space: pre-wrap">
      {{ item }}
    </div>
  </el-dialog>
</template>

<script setup>
import { ref } from 'vue'
import { ElDialog } from 'element-plus'

const visible = ref(false)

const text = ref([])
const title = ref('')

const show = ({ name }, content) => {
  text.value = formatTest(content)
  console.log('text', text.value)
  title.value = name
  visible.value = true
}

const formatTest = (str) => {
  if (str && str.length > 0) {
    return str.split('<>')
  } else {
    return ['']
  }
}

defineExpose({ show })
</script>

<style lang="scss" scoped></style>
