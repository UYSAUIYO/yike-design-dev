<script setup lang="ts">
import { getCurrentInstance } from 'vue'

const props = defineProps({
  fileContent: {
    type: Object,
    default: () => {
      return {}
    },
  },
  progress: {
    type: Number,
    default: 0,
  },
})
const { proxy }: any = getCurrentInstance()

const emits = defineEmits(['handleAbort', 'handleRemove', 'handleReUpload'])
// const handlePause = () => {
//   emits('handleAbort')
// }
const handleRemove = () => {
  emits('handleRemove', props.fileContent)
}
const handleReview = () => {
  proxy.$message({ type: 'success', message: '此处使用图片组件进行预览' })
}
// const handleReUpload = (fileContent: any) => {
//   emits('handleReUpload', fileContent)
// }
</script>
<template>
  <div class="yk-image-content">
    <img :src="fileContent.url" alt="" />
    <div class="overlay"></div>
    <div class="overlay-icons">
      <Icon class="preview-icon" name="yk-yanjing" @click="handleReview"></Icon>
      <Icon class="delete-icon" name="yk-shanchu" @click="handleRemove"></Icon>
    </div>
  </div>
</template>
<style lang="less" scoped>
@import '../../assets/style/yk-index.less';

.yk-image-content {
  width: 80px;
  height: 80px;
  margin-right: 40px;
  background: @bg-color-m;
  border-radius: 8px;
  overflow: hidden;
  margin-bottom: 10px;
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  background-color: #000;
  transition: opacity 0.3s ease;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}
.overlay-icons {
  width: 64px;
  height: 14px;
  position: absolute;
  font-size: 16px;
  visibility: hidden;
  left: 50%;
  top: 50%;
  color: @bg-color-l;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  svg {
    cursor: pointer;
  }
}
.yk-image-content:hover .overlay {
  opacity: 0.5;
}
.yk-image-content:hover .overlay-icons {
  visibility: visible;
}
</style>
