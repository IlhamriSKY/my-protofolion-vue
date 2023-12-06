<template>
    <section class="cta__area p-relative z-index-1">
        <div class="container">
            <div class="cta__wrapper-2 p-relative">
                <div class="cta__shape">
                    <img class="cta__shape-1" src="assets/img/user/cta-shape-1.png" alt="cta__shape" />
                    <img class="cta__shape-2" src="assets/img/user/cta-shape-2.png" alt="cta__shape" />
                    <img class="cta__shape-3" src="assets/img/cta/2/cta-shape-3.png" alt="cta__shape" />

                    <!-- <div class="circle-wrap">
                        <div class="circle-image">
                            <img src="assets/img/user/ilhamtext.png" alt="circle-image">
                        </div>
                    </div> -->

                </div>
                <div class="row align-items-center">
                    <div class="col-xxl-6 col-lg-6">


                        <div class="cta__thumb-2">
                            <img  width="350" v-lazy="'assets/img/user/ilham.jpg'"
                                alt="cta_thumbnail" />
                        </div>

                    </div>
                    <div class="col-xxl-6 col-lg-6">
                        <div class="cta__content-2">
                            <h3>
                                {{ trans('Empowering Front-End Magic with Expert Back-End Mastery') }}
                            </h3>
                            <p>
                                {{ trans(`Backend Developer with 3 years of experience. Proficient in creating web
                                applications,
                                chatbots, and APIs. Good knowledge in PHP, Python, and JavaScript. Experienced in
                                using Laravel and building chatbots. Familiar with collaborative development using Git.
                                Passionate about creating efficient and scalable solutions.`) }}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script setup>
"use strict";
const props = defineProps(['cta'])
import Tilt from 'vanilla-tilt-vue'

const options = {
    glare: false,
}
</script>
<style>
.circle-wrap .circle-image {
    width: 100%;
    max-width: 150px;
    aspect-ratio: 1/1;
    position: absolute;
    top: 85%;
    left: 35%;
    transform: translate(-50%, -50%);
    filter: brightness(0) invert(1);
    mix-blend-mode: exclusion;
    z-index: 99;
}

.circle-wrap .circle-image img {
    width: 100%;
    animation: rotate360 15s linear infinite forwards;
}

@keyframes rotate360 {
    100% {
        transform: rotate(360deg);
    }
}
</style>
