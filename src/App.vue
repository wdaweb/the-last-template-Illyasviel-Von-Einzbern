<template>
  <v-app>
    <v-main>
      <v-container>
        <v-app-bar app color="primary" dark>
          <v-app-bar-nav-icon @click="onMenuClick" />
          <v-toolbar-title>DBD</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn text>AAA</v-btn>
          <v-btn text>BBB</v-btn>
          <v-btn text>CCC</v-btn>
        </v-app-bar>

        <swiper :autoplay="{
          delay: 5000,
          disableOnInteraction: false,
        }" :breakpoints="{
            576: {
              slidesPerView: 1,
              spaceBetween: 20,
            },
            768: {
              slidesPerView: 1,
              spaceBetween: 20,
            },
            900: {
              slidesPerView: 1,
              spaceBetween: 20,
            },
            1200: {
              slidesPerView: 2,
              spaceBetween: 20,
            },
            1400: {
              slidesPerView: 2,
              spaceBetween: 20,
            },
          }" class="mySwiper" :keyboard="{
            enabled: true,
          }" :loop="true" :modules="modules" :mousewheel="true" :navigation="true" :pagination="{ clickable: true }"
          :scrollbar="{ draggable: true }" :slides-per-view="1" :space-between="30">
          <!-- 資料要顯示在畫面(view)上，要將元件綁定資料 -->
          <swiper-slide><img src="https://picsum.photos/800/600/?random=1"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=2"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=3"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=4"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=5"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=6"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=7"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=8"></swiper-slide>
          <swiper-slide><img src="https://picsum.photos/800/600/?random=9"></swiper-slide>
        </swiper>
      </v-container>
      <v-container>
        <v-row>
          <v-col cols="12" md="4">
            <v-card
              class="mx-auto card_test"
              max-width="344"
            >
              <v-img
                height="200px"
                src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
                cover
              ></v-img>

              <v-card-title>
                Top western road trips
              </v-card-title>

              <v-card-subtitle>
                1,000 miles of wonder
              </v-card-subtitle>

              <v-spacer></v-spacer>

            </v-card>
          </v-col>
          <v-col cols="12" md="4">
            <v-card
              class="mx-auto card_test"
              max-width="344"
            >
              <v-img
                height="200px"
                src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
                cover
              ></v-img>

              <v-card-title>
                Top western road trips
              </v-card-title>

              <v-card-subtitle>
                1,000 miles of wonder
              </v-card-subtitle>
            </v-card>
          </v-col>
          <v-col cols="12" md="4">
            <v-card
              class="mx-auto card_test"
              max-width="344"
            >
              <v-img
                height="200px"
                src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
                cover
              ></v-img>

              <v-card-title>
                Top western road trips
              </v-card-title>

              <v-card-subtitle>
                1,000 miles of wonder
              </v-card-subtitle>

              <v-card-actions>
                <v-btn
                  color="orange-lighten-2"
                  text="Explore"
                ></v-btn>

                <v-spacer></v-spacer>

                <v-btn
                  :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                  @click="show = !show"
                ></v-btn>
              </v-card-actions>

              <v-expand-transition>
                <div v-show="show">
                  <v-divider></v-divider>

                  <v-card-text>
                     Lorem ipsum dolor sit amet consectetur
                  </v-card-text>
                </div>
              </v-expand-transition>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="4">
            <v-card subtitle="This is a card subtitle"
              text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus!"
              title="This is a title"
              image="https://picsum.photos/800/600/?random=10">
            </v-card>
          </v-col>
          <v-col cols="12" md="4">
            <v-card subtitle="This is a card subtitle"
              text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus!"
              title="This is a title">
            </v-card>
          </v-col>
          <v-col cols="12" md="4">
            <v-card subtitle="This is a card subtitle"
              text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus!"
              title="This is a title">
            </v-card>
          </v-col>
        </v-row>

      </v-container>
    </v-main>
  </v-app>
     <div ref="box" class="box">Hello</div>
     <Live2D/>
</template>

<script setup>
  import { A11y, Autoplay, Keyboard, Mousewheel, Navigation, Pagination, Scrollbar } from 'swiper/modules'
  // 引入 Swiper 核心跟模組
  import { Swiper, SwiperSlide } from 'swiper/vue'
  // 引入 Swiper 和 SwiperSlide 元件
  import 'swiper/css'
  // 引入 swiper 的 css 樣式
  import 'swiper/css/navigation'
  // 引入 swiper 導航樣式
  import 'swiper/css/pagination'
  // 引入 swiper 分頁模式
  import 'swiper/css/scrollbar'
  // 引入 swiper

  import { gsap } from "gsap";

  // import SplitText from './gsap/SplitText';
  // gsap.registerPlugin(SplitText)

  import { ref, onMounted } from 'vue';

  import Live2D from './Live2D.vue'

const box = ref(null)

  onMounted(() => {
    gsap.to(box.value, {
      duration: 10,
      x: 200,
      y: 200,
      rotation: 3600
    })
  })
</script>

<style scoped>
  .mySwiper{
    width: 800px;
    height: 400px;
  }
  .mySwiper{
    /* width: 100%; */
    /* height: 100%; */
    object-fit: cover;
    /* 確保元素填滿容器 */
  }
  .box {
    width: 100px;
    height: 100px;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>



