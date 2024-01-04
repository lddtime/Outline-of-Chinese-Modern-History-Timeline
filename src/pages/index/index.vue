<template>
  <uni-nav-bar dark title="中国近现代史纲要时间轴" right-icon="settings" @clickRight="onClickRight"></uni-nav-bar>
  <view class="body">
    <view v-if="error" class="text-area">
      <text class="title">{{ error }}</text>
    </view>
    <zero-timeline v-else :dataList="history" gap="30px" />
  </view>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const history = ref([])
const error = ref(null)

fetch('/static/history.json')
  .then((res) => res.json())
  .then((json) => (history.value = json))
  .catch((err) => (error.value = err))

// f94144-f3722c-f8961e-f9844a-f9c74f-90be6d-43aa8b-4d908e-577590-277da1-6a4c93
// 54478c-2c699a-048ba8-0db39e-16db93-83e377-b9e769-efea5a-f1c453-f29e4c-ee6055
function onClickRight() {
  console.log('onClickRight');
}
</script>

<style>
.body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: auto;
}

@media (min-width: 1024px) {
  .body {
    max-width: 50%;
  }
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}
</style>
