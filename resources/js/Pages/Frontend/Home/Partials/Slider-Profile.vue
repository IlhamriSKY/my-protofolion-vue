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
    glare: true,
    "max-glare": 2,
    scale: 1.1,
    "glare-prerender": false,
    gyroscope: true,
}
</script>

<template>
    <SliderSkeleton v-if="loading" />
    <section class="slider__area pb-140 pt-120 p-relative fix">
        <div class="slider__active-2 slider__bid-area" v-show="sliders.length > 0 && !loading">
            <div class="single-slider d-flex align-items-center">
                <div class="container">
                    <div class="row">
                        <div class="col-xxl-6 col-xl-6 col-lg-6">
                            <div class="slider__content-2">
                                <h4 class="slider__title-2">
                                    {{ trans('Empowering') }}, <span> {{ trans('Front-End') }}</span>
                                    {{
                                        trans(`Magic with Expert`)
                                    }}
                                    <span class="has-shape">
                                        {{ trans('Back-End') }}
                                        <img class="slider-title-shape" src="assets/img/icon/slider-stoke-shape.svg"
                                            alt="title" />
                                    </span>
                                    {{ trans('Mastery') }}
                                </h4>
                                <p>
                                    {{
                                        trans(`If you are an artist and want to be a successful artist then
                                    learn to how to create digital art with prompt.`)
                                    }}
                                </p>


                                <div class="slider__btn-2 d-sm-flex align-items-center">
                                    <Link :href="route('about')" class="tp-btn-border text-white header-button active mr-15 mb-15">
                                    {{ trans('About') }}
                                    </Link>
                                    <Link :href="route('download.cv')" class="tp-btn-borde mb-15">
                                    {{ trans('Download CV') }}
                                    </Link>
                                </div>

                            </div>
                        </div>
                        <div class="col-xxl-6 col-xl-6 col-lg-6">
                            <div class="slider__bid-item pl-70">
                                <div class="slider__bid-item-bg"></div>
                                <Tilt :parallax="true" :options="options">
                                    <Swiper @slideChange="onSwiper" style="z-index: -10" :slides-per-view="1"
                                        :space-between="10" :modules="modules" :navigation="navigationOptions" :loop="true"
                                        :effect="'fade'">
                                        <SwiperSlide class="slider__bid-thumb" v-for="slider in sliders" :key="slider">
                                            <img width="350" :src="slider.preview" alt="preview" />
                                        </SwiperSlide>
                                    </Swiper>
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
</style>
