<template>
  <view class="content">
    <WeappTailwindcss></WeappTailwindcss>

    <view class="text-gray-900/50 mb-2 before:content-['当前系统主题:']">
      {{ themeRef }}
    </view>
    <view class="space-y-[20rpx] flex flex-col items-center">
      <view
        class="bg-[#010101] h-16 w-16 rounded-[20rpx] text-white flex justify-center items-center after:content-['hover']"
        hover-class="bg-[gray] after:!content-['good!']"></view>
      <view
        class="grid grid-cols-3 divide-x-[10px] divide-[#010101] divide-solid">
        <div :class="classArray">1</div>
        <div>2</div>
        <div :class="classArray">3</div>
      </view>
      <view
        class="w-32 py-2 rounded-md font-semibold text-white bg-pink-500 ring-4 ring-pink-300">
        Default
      </view>
      <view>
        <button class="text-[#fff]" :class="buttonClass" @click="increment">
          click here to inc {{ count }}
        </button>
      </view>

      <view class="test">@apply</view>
    </view>
  </view>
</template>

<script setup lang="ts">
import WeappTailwindcss from '@/components/WeappTailwindcss.vue'
import { useCounterStore } from '@/stores/counter'

const store = useCounterStore()
const { count } = storeToRefs(store)
const { increment } = store
const buttonColors = [
  'bg-[#000]',
  'bg-[#111]',
  'bg-[#222]',
  'bg-[#333]',
  'bg-[#444]',
  'bg-[#555]',
  'bg-[#666]',
  'bg-[#777]',
  'bg-[#888]',
  'bg-[#999]',
  'bg-[#aaa]',
  'bg-[#bbb]',
  'bg-[#ccc]',
  'bg-[#ddd]',
  'bg-[#eee]',
  'bg-[#fff]'
]
const title = ref('Hello')
const themeRef = ref(uni.getSystemInfoSync().theme)
const classArray = computed(() => [
  title.value ? 'bg-[#ff00ff]' : undefined,
  {
    'text-[#00ffff]': Boolean(title),
    "bg-[url('https://xxx.com/xx.webp')]": true,
    "bg-[url('https://yyyy.com/ccc.webp')]": true
  }
])
const buttonClass = computed(() => {
  return buttonColors[count.value % buttonColors.length]
})
// #ifdef MP
uni.onThemeChange(({ theme }: { theme: 'dark' | 'light' }) => {
  themeRef.value = theme
})
// #endif
onBeforeUnmount(() => {
  // #ifdef MP
  uni.offThemeChange(() => {
    console.log('offThemeChange')
  })
  // #endif
})

onLoad(() => {
  console.log('欢迎使用uni-app-vite-vue3-tailwindcss模板')
})
</script>

<style lang="scss" scoped>
.logo {
  @apply h-[100rpx] w-[100rpx];
}

.content {
  @apply flex flex-col items-center;
}

.test {
  @apply flex items-center justify-center h-[100px] w-[100px] rounded-[40px] bg-[#123456] bg-opacity-[0.54] text-[#ffffff] #{!important};
}
</style>
