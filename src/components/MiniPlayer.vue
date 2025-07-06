<template>
  <div class="fixed bottom-5 right-5 z-50 w-72 bg-white/10 text-white backdrop-blur-xl p-4 rounded-2xl shadow-lg flex flex-col gap-2">
    <!-- 歌曲标题 -->
<!--    <div class="font-bold text-sm truncate">{{ title }}</div>-->

    <!-- 控制区 -->
    <div class="flex items-center justify-between">
      <!-- 播放按钮 -->
      <button @click="togglePlay" class="text-white hover:text-yellow-300 transition">
        <!-- ▶️ 播放图标 -->
        <svg v-if="!isPlaying" xmlns="http://www.w3.org/2000/svg" class="w-3 h-3" viewBox="0 0 24 24">
          <path d="M5 3v18l15-9L5 3z"/>
        </svg>

        <!-- ⏸️ 暂停图标 -->
        <svg v-else xmlns="http://www.w3.org/2000/svg" class="w-3 h-3" viewBox="0 0 24 24">
          <path d="M6 4h4v16H6zm8 0h4v16h-4z"/>
        </svg>
      </button>

      <!-- 进度条 -->
      <input
        type="range"
        min="0"
        :max="duration"
        step="0.1"
        v-model="currentTime"
        @input="seek"
        class="w-full mx-3 accent-white"
      />

      <!-- 音量控制 -->
      <input
        type="range"
        min="0"
        max="1"
        step="0.01"
        v-model="volume"
        class="w-16 accent-white"
      />
    </div>

    <!-- 隐藏 audio 标签 -->
    <audio
      ref="audioRef"
      :src="src"
      autoplay
      muted
      loop
      @timeupdate="updateTime"
      @canplay="initAudio"
    />
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const props = defineProps({
  src: { type: String, required: true },
  title: { type: String, default: '背景音乐' }
})

const audioRef = ref(null)
const isPlaying = ref(false)
const currentTime = ref(0)
const duration = ref(0)
const volume = ref(0.4)

onMounted(() => {
  // 等用户第一次点击页面再取消静音
  const enableAudio = () => {
    if (audioRef.value) {
      audioRef.value.muted = false
      audioRef.value.volume = volume.value
    }
    document.removeEventListener('click', enableAudio)
  }
  document.addEventListener('click', enableAudio)
})

const togglePlay = () => {
  if (!audioRef.value) return
  if (isPlaying.value) {
    audioRef.value.pause()
  } else {
    audioRef.value.play()
  }
  isPlaying.value = !isPlaying.value
}

const updateTime = () => {
  if (!audioRef.value) return
  currentTime.value = audioRef.value.currentTime
}

const seek = () => {
  if (audioRef.value) {
    audioRef.value.currentTime = currentTime.value
  }
}

watch(volume, (val) => {
  if (audioRef.value) {
    audioRef.value.volume = val
  }
})

const initAudio = () => {
  if (audioRef.value) {
    duration.value = audioRef.value.duration
  }
}
</script>

<style scoped>
input[type='range'] {
  height: 4px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
