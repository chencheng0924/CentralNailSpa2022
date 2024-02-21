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
import { getAssetsFileIcon } from '@/utils/commonUse.js'
const optionList = ref(['HOME', 'SERVICES', 'GALLERY', 'CONTACT US'])
const iconList = ref(['NAILS', 'WAXING', 'EYELASH', 'FACIAL', 'BACK & FEET RELAXING'])
</script>

<template>
  <div class="wrapper">
    <div class="header">
      <div class="section1">
        <div class="section1Title">Central Nail Spa 2022</div>
        <div class="optionList">
          <div v-for="(item, index) in optionList" :key="index">{{ item }}</div>
        </div>
      </div> 
      <div class="section2">Polish your life <hr>with perfect nails!</div>
      <div class="section3"><img src="../assets/img/1.jpg" alt=""></div>
      <div class="paintWall" />
    </div>
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
    <div class="fixed top-0 left-0 w-screen h-screen flex items-center justify-center pic z-10" v-if="showBigPhoto">
      <div class="absolute right-10 top-5 text-xl font-semibold z-20 text-white cursor-pointer" @click="showBigPhoto = false">CLOSE</div>
       <img src="@/assets/img/ca.png" class="rotate-180 w-[50px] absolute top-[50%] left-[10%] translate-y-[-50%] cursor-pointer" v-if="nowIndex > 1" @click="changePicIndex('back')">
      <img :src="nowPic" class="w-[70vw] h-[80vh] object-contain">
      <img src="@/assets/img/ca.png" class="w-[50px] absolute top-[50%] right-[10%] translate-y-[-50%] cursor-pointer" v-if="nowIndex < pLimit" @click="changePicIndex('go')">
    </div>
    <div class="servicePrice">
      <div class="store"><img src="../assets/img/store.png" alt=""></div>
      <div class="service"><img src="../assets/img/service.png" alt=""></div>
    </div>
    <div class="menu"><img src="../assets/img/menu.png" alt=""></div>
    <!-- Nails Transformed, Beauty Defined. -->
    <div class="w-screen flex items-center flex-col py-5 px-20" >
      <span class="text-[#865105] text-[32px] font-bold mb-5" style="font-family: 'InriaSans';letter-spacing: 5px;">Nails Transformed, Beauty Defined.</span>
      <div class="max-w-[1200px] flex flex-wrap gap-5 justify-between">
        <img :src="getAssetsFile(`c${pic}.png`)" alt="" v-for="pic in 10" class="w-[191px] h-[250px] object-cover" @click="show('c', pic, 10)">
      </div>
      <div class="w-[1280px] flex flex-wrap gap-3 justify-between mt-5 px-20">
       <img :src="getAssetsFile(`d${pic}.png`)" alt="" v-for="pic in 4" class="w-[260px] h-[168px] object-cover" @click="show('d', pic, 4)">
      </div>
    </div>
    <!-- NAIL IT WITH STYLE! -->
    <div class="w-screen flex">
      <img src="@/assets/img/pp.png" alt="" class="w-[30%] object-cover">
      <div class="w-[80%] bg-[#E5D6CD] flex flex-col items-center justify-center gap-5">
        <span class="leading-[38.22px] text-[32px] font-bold mb-5" style="font-family: JosefinSlab;letter-spacing: 5px;">NAIL IT WITH STYLE!</span>
        <div class="flex gap-5 items-center">
          <img src="@/assets/img/ig.svg" alt="" class="w-[58px] h-[58px] mr-5">
          <div class="flex flex-col items-center justify-between">
            <span class="text-[24px]" style="font-family: KaushanScript;letter-spacing: 5px;">Follow & Share</span>
            <a href="https://www.instagram.com/centralnail745/" target="_blank" class="underline text-[24px]" style="font-family: KaiseiDecol;letter-spacing: 2px;">@Centralnailspa2022</a>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="iconList">
        <div v-for="(item, index) in iconList" :key="index">
          <img :src="getAssetsFileIcon(`${index + 1}.svg`)" alt="">
          {{ item }}
        </div>
      </div>
      <div class="footerSection">
        <div class="footerContent">
          <div class="section1">
            <div class="title">Central Nail Spa 2022</div>
            <div>+1 631-521-6999</div>
            <div>745 Commack Rd, Brentwood, NY <hr>11717, United States</div>
          </div>
          <div class="section2">
            <div class="time">OPENING HOURS</div>
            <div>Monday - Saturday<hr>10:00 - 19:30</div>
            <div>Sunday<hr>10:00 - 18:00</div>
          </div>
          <div class="section3">
            <div v-for="(item, index) in optionList" :key="index">{{ item }}</div>
          </div>
        </div>
        <div class="footerImg"><img src="../assets/img/footerImg.svg" alt=""></div>
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
.wrapper{
  display: flex;
  flex-direction: column;
  gap: 50px;
}
.header {
  padding: 80px 120px;
  background-color: #E5D6CD;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 50px;
  position: relative;
  .paintWall{
    position: absolute;
    bottom: 0;
    background-color: #fff;
    width: 100%;
    height: 180px;
    z-index: 3;
  }
  .section1{
    width: 100%;
    display: flex;
    justify-content: space-between;
    .section1Title{
      font-weight: 700;
      font-size: 18px;
    }
    .optionList{
      display: flex;
      gap: 30px;
      >div{
        font-size: 14px;
        font-weight: 400;
        cursor: pointer;
      }
    }
  }
  .section2{
    font-size: 40px;
    font-weight: 400;
    font-family: Jomolhari;
    letter-spacing: 10px;
    text-align: center;
  }
  .section3{
    z-index: 5;
    img{
      width: 620px;
      height: 336px;
    }
  }
}
.servicePrice{
  display: flex;
  align-items: center;
  .store{
    width: 50%;
    height: 479px;
    z-index: 3;
    img{
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }
  .service{
    width: 50%;
    display: flex;
    justify-content: center;
    background-color: #E5D6CD;
    position: relative;
    img{
      object-fit: contain;
    }
    &::before{
      z-index: 2;
      position: absolute;
      left: -300px;
      top: 0;
      content: '';
      display: block;
      height: 100%;
      width: 300px;
      background-color: #E5D6CD;
    }
  }
}
.menu{
  width: 100%;
}
.footer{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  // padding: 50px 0 0 ;
  gap: 50px;
  .iconList{
    padding: 0 120px;
    display: flex;
    align-items: center;
    gap: 80px;
    >div{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      font-family: Jomolhari;
      gap: 10px;
      img{
        width: 125px;
        height: 125px;
      }
    }
  }
  .footerSection{
    display: flex;
    align-items: center;
    width: 100%;
    height: 341px;
    .footerContent{
      background-color: #E5D6CD;
      width: 60%;
      height: 100%;
      display: flex;
      justify-content: space-evenly;
      align-items: center;
      .section1{
        display: flex;
        flex-direction: column;
        gap: 10px;
        >div{
          font-family: 'KaiseiDecol';
          font-size: 14px;
          font-weight: 400;
        }
        .title{
          font-weight: 700;
          font-size: 24px;
          font-family: Jomolhari;
        }
      }
      .section2{
        display: flex;
        flex-direction: column;
        gap: 5px;
        >div{
          font-family: 'KaiseiDecol';
          font-size: 14px;
          font-weight: 400;
        }
        .time{
          font-size: 16px;
        }
      }
      .section3{
        >div{
          font-family: 'KaiseiDecol';
          font-size: 14px;
          font-weight: 400;
          cursor: pointer;
        }
        display: flex;
        flex-direction: column;
        gap: 20px;
      }
    }
    .footerImg{
      width: 40%;
      height: 100%;
      img{
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }
  }
}
</style>