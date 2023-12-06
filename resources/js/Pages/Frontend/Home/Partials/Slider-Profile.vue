<script setup>
"use strict";
import sharedComposable from '@/composables/sharedComposable'
import { Navigation, EffectFade } from 'swiper'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { onMounted, ref, computed } from 'vue'
import axios from 'axios'
import SliderSkeleton from './SliderSkeleton.vue'

// swiper styles
import 'swiper/css'
import 'swiper/css/navigation'
import 'swiper/css/effect-fade'
import { router } from '@inertiajs/vue3'

import Tilt from 'vanilla-tilt-vue'

const navigationOptions = {
    nextEl: '.slider-button-next',
    prevEl: '.slider-button-prev'
}
const modules = [Navigation, EffectFade]
const sliders = ref([])
const sliderIndex = ref(0)
const loading = ref(false)
const { formatCurrency, authUser, ToastAlert, textExcerpt } = sharedComposable()

const getSlider = () => {
    axios.get(route('api-home-two', { type: 'slider' })).then((res) => {
        sliders.value = res.data
        loading.value = false
    })
}
onMounted(() => {
    loading.value = true

    getSlider()
})
const onSwiper = (swiper) => {
    sliderIndex.value = swiper.realIndex
}

const findSlider = computed(() => {
    return sliders.value[sliderIndex.value]
})
const like = (id) => {
    if (!authUser.value) {
        return router.get(route('login'))
    }
    router.post(
        route('user.like'),
        { id: id },
        {
            preserveScroll: true,
            onSuccess: () => {
                getSlider()
                ToastAlert(
                    `${findSlider.value?.is_liked === 0 ? 'Like' : 'Disliked'} Successfully`,
                    `${findSlider.value?.is_liked === 0 ? 'Like' : 'Disliked'} Successfully`
                )
            }
        }
    )
}

const options = {
    glare: false,
    scale: 1,
    gyroscope: true,
    max: 25,
}
</script>

<template>
    <SliderSkeleton v-if="loading" />
    <section class="slider__area pb-140 pt-120 p-relative fix">
        <div class="slider__active-2 slider__bid-area" v-show="sliders.length > 0 && !loading">

            <div class="slider__shape">
                <img class="slider__shape-1" src="assets/img/slider/2/slider-shape-1.png" alt="slider__shape" />
                <img class="slider__shape-2" src="assets/img/slider/2/slider-shape-2.png" alt="slider__shape" />
            </div>

            <div class="single-slider d-flex align-items-center">
                <div class="container">
                    <div class="row">
                        <div class="col-xxl-6 col-xl-6 col-lg-6">
                            <div class="slider__content-2">
                                <h3 class="slider__title-sm">
                                    <span class="wave">👋</span> {{ trans('Hello, My Name Is Ilham') }}
                                </h3>

                                <h3 class="slider__title-2">
                                    {{ trans('I am') }}

                                    <span class="has-shape">
                                        {{ trans('BACK-END') }}
                                        <img class="slider-title-shape" src="assets/img/icon/slider-stoke-shape.svg"
                                            alt="title" />
                                    </span>

                                    {{ trans('DEVELOPER') }}
                                </h3>

                                <h3 class="slider__title-3">
                                    {{ trans(`I've been developing websites for 3 years, specializing in web applications,
                                    chatbots, and APIs. I'm skilled in PHP, Python, and JavaScript, with expertise in
                                    Laravel and chatbot development. I'm also experienced in collaborative coding using Git.
                                    My focus is on crafting efficient and scalable solutions.`) }}
                                </h3>


                                <div class="d-sm-flex align-items-center mt-4">
                                    <button @click="scrollToEl1" class="tp-btn-border header-button active mr-15 mb-15">
                                        {{ trans('About') }}
                                    </button>

                                    <a :href="route('download.cv')" class="tp-btn-border active mr-15 mb-15">{{
                                        trans("Download CV") }}</a>
                                </div>

                            </div>
                        </div>
                        <div class="col-xxl-6 col-xl-6 col-lg-6">
                            <div class="slider__bid-item pl-70">
                                <div class="slider__bid-item-bg"></div>
                                <Tilt data-tilt-full-page-listening :parallax="true" :options="options">
                                    <div class="product__details-thumb-content">
                                        <img width="350" v-lazy="'assets/img/user/ilham.jpg'">

                                    </div>
                                </Tilt>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style>
.header-button {
    background-color: var(--tp-common-white);
    color: var(--tp-common-black);
    -webkit-box-shadow: 0px 6px 20px rgba(255, 255, 255, 0.24);
    -moz-box-shadow: 0px 6px 20px rgba(255, 255, 255, 0.24);
    -ms-box-shadow: 0px 6px 20px rgba(255, 255, 255, 0.24);
    -o-box-shadow: 0px 6px 20px rgba(255, 255, 255, 0.24);
    box-shadow: 0px 6px 20px rgba(255, 255, 255, 0.24);
}

.active-light-mode .header-button {
    background-color: var(--tp-common-black);
    color: var(--tp-common-white);
    -webkit-box-shadow: 0px 2px 50px rgba(185, 0, 145, 0.5);
    -moz-box-shadow: 0px 2px 50px rgba(185, 0, 145, 0.5);
    -ms-box-shadow: 0px 2px 50px rgba(185, 0, 145, 0.5);
    -o-box-shadow: 0px 2px 50px rgba(185, 0, 145, 0.5);
    box-shadow: 0px 1px 50px rgba(185, 0, 145, 0.5);
}

.active-light-mode .header-button:hover {
    background-color: var(--tp-common-white);
    color: var(--tp-common-black);
}

.header-button:hover {
    background-color: var(--tp-common-black);
    color: var(--tp-common-white);
}

.slider__title-sm {
    font-size: 18px;
    font-weight: 200;
    margin-bottom: 0;
    color: var(--tp-common-white);
}

.active-light-mode .slider__title-sm {
    font-size: 18px;
    font-weight: 200;
    margin-bottom: 0;
    color: var(--tp-common-black);
}

.active-light-mode .slider__title {
    font-size: 30px;
    font-weight: 700;
    color: var(--tp-common-black);
    margin-bottom: 0;
}

.slider__title-3 {
    font-size: 20px;
    font-weight: 200;
    color: var(--tp-common-white);
    margin-bottom: 0;
}

.active-light-mode .slider__title-3 {
    font-size: 20px;
    font-weight: 200;
    color: var(--tp-common-black);
    margin-bottom: 0;
}</style>
