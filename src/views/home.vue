<script setup>
import { ref, onMounted, reactive, computed } from 'vue'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'
import { getAssetsFile } from '@/utils/commonUse'
components: {
  Carousel,
  Slide,
  Pagination,
  Navigation
}
const showBigPhoto = ref(false)
const p = ref('')
const pType = ref('')
const pLimit = ref(0)
const nowIndex = ref(0)
const nowPic = computed(() => {
  return getAssetsFile(`${p.value}.png`)
})
const show = (type, idx, limit) => {
  pLimit.value = limit
  pType.value = type
  showBigPhoto.value = true
  nowIndex.value = idx
  p.value = type + idx.toString()
}
const breakpoints = {
  // 700px and up
  700: {
    itemsToShow: 3.5,
    snapAlign: 'center',
  },
  // 1024 and up
  1024: {
    itemsToShow: 5,
    snapAlign: 'start',
  },
}
const changePicIndex = (type) => {
  type == 'back' ? nowIndex.value -= 1 : nowIndex.value += 1
  let n = nowIndex.value
  p.value = pType.value + n.toString()
}
</script>
<style>
</style>
<template>
  <!-- 輪播 -->
  <div class="w-screen py-10 flex flex-col items-center">
    <div class="max-w-[1200px]">
      <Carousel :snapAlign="'center'" :breakpoints="breakpoints">
        <Slide v-for="slide in 10" :key="slide" @click="show('m', slide, 10)">
          <div class="carousel__item">
            <!-- <img :src="getAssetsFile(`m${slide}.png`)" class="w-[200px]"> -->
            <img :src="getAssetsFile(`m${slide}.png`)" class="w-[220px] h-[281px] object-cover">
          </div>
        </Slide>
        <template #addons>
          <Navigation />
        </template>
      </Carousel>
    </div>
  </div>
  <div class="fixed top-0 left-0 w-screen h-screen flex items-center justify-center pic" v-if="showBigPhoto">
    <div class="absolute right-10 top-5 text-xl font-semibold z-20 text-white cursor-pointer" @click="showBigPhoto = false">CLOSE</div>
    <img src="@/assets/img/ca.png" class="rotate-180 w-[50px] absolute top-[50%] left-[10%] translate-y-[-50%] cursor-pointer" v-if="nowIndex > 1" @click="changePicIndex('back')">
    <img :src="nowPic" class="w-[70vw] h-[80vh] object-contain">
    <img src="@/assets/img/ca.png" class="w-[50px] absolute top-[50%] right-[10%] translate-y-[-50%] cursor-pointer" v-if="nowIndex < pLimit" @click="changePicIndex('go')">
  </div>
  <!-- Nails Transformed, Beauty Defined. -->
  <div class="w-screen flex items-center flex-col py-5">
    <span class="text-[#865105] text-[32px] font-bold mb-5">Nails Transformed, Beauty Defined.</span>
    <div class="max-w-[1200px] flex flex-wrap gap-5 justify-between">
      <img :src="getAssetsFile(`c${pic}.png`)" alt="" v-for="pic in 10" class="w-[220px] h-[280px] object-cover" @click="show('c', pic, 10)">
    </div>
    <div class="w-[1280px] flex flex-wrap gap-3 justify-between mt-5">
      <img :src="getAssetsFile(`d${pic}.png`)" alt="" v-for="pic in 4" class="w-[300px] h-[188px] object-cover" @click="show('d', pic, 4)">
    </div>
  </div>
  <!-- NAIL IT WITH STYLE! -->
  <div class="w-screen flex">
    <img src="@/assets/img/pp.png" alt="" class="w-[20%] object-cover">
    <div class="w-[80%] bg-[#E5D6CD] flex flex-col items-center justify-center gap-5">
      <span class="leading-[38.22px] text-[32px] font-bold">NAIL IT WITH STYLE!</span>
      <div class="flex gap-5 items-center">
        <img src="@/assets/img/ig.svg" alt="" class="w-[58px] h-[58px]">
        <div class="flex flex-col items-center justify-between">
          <span class="text-[24px]">Follow & Share</span>
          <a href="https://www.instagram.com/centralnail745/" target="_blank" class="underline text-[24px]">@Centralnailspa2022</a>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="scss" scoped>
:deep(.carousel__prev) {
  left: -45px;
}

:deep(.carousel__next) {
  right: -45px;
}

.pic {
  background-color: rgba(0,0,0,0.7);
}
</style>