<script setup lang="ts">
import { onMounted, reactive } from 'vue'
import dayjs from 'dayjs'

function goPage() {
  window.location.href = 'https://ow.blizzard.cn/returns'
}

const restDate = reactive({
  day: 0,
  hour: 0,
  minute: 0,
  second: 0,
})

const releaseDate = dayjs('2022-10-05')

function getRestDate() {
  const now = dayjs()
  const restSecond = releaseDate.diff(now, 'second')
  restDate.day = Math.floor(restSecond / (60 * 60 * 24))
  restDate.hour = Math.floor((restSecond % (60 * 60 * 24)) / (60 * 60))
  restDate.minute = Math.floor((restSecond % (60 * 60)) / 60)
  restDate.second = Math.floor(restSecond % 60)
}

onMounted(() => {
  setInterval(() => {
    getRestDate()
  }, 1000)
})
</script>

<template>
  <div flex="~ col" h-full justify-center>
    <div text-9 flex="~ wrap" gap="3" items-center justify-center>
      <div>距离</div>
      <img cursor-pointer h-14 src="/logo.png" alt="" @click="goPage">
      <div>归来发布还剩</div>
    </div>
    <div text-8>
      {{ restDate.day }} 天 {{ restDate.hour }} 小时 {{ restDate.minute }} 分 {{ restDate.second }} 秒
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>
