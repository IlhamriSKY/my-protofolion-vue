<script setup>
"use strict";
import { nextTick, ref } from "vue"
import VueWriter from "vue-writer";

import ConfettiExplosion from "vue-confetti-explosion";

const visible = ref(false);

const explode = async () => {
    visible.value = false;
    await nextTick();
    visible.value = true;
};

const colors = ['#1c3faa'];

const loading = ref(false);
const arr = ["Portfolio", "Information", "Blog"];
</script>

<template>
    <SliderSkeleton v-if="loading" />
    <section v-if="!loading"
        class="slider__area pt-40 pb-70 p-relative slider__height-3 d-flex align-items-center p-relative fix">

        <div class="slider__shape">
            <img class="slider__shape-1" src="assets/img/slider/2/slider-shape-1.png" alt="slider__shape" />
            <img class="slider__shape-2" src="assets/img/slider/2/slider-shape-2.png" alt="slider__shape" />
        </div>

        <div class="container">
            <div class="row justify-content-center">
                <div class="col-xxl-10">
                    <div class="slider__content-3">
                        <div class="slider__search text-center">
                            <span>
                                <span class="wave">👋</span> Hello, My Name Is <button @click="explode">Ilham</button>
                                <ConfettiExplosion stageHeight="450" stageWidth="400" v-if="visible" :colors="colors"
                                    class="confetti-above" />
                            </span>
                            <h3 class="slider__title-3">
                                <vue-writer :array="arr" :eraseSpeed="50" :typeSpeed="100" :delay="1000">
                                    {{ trans("Welcome to My ") }}
                                </vue-writer>
                            </h3>
                            <span>
                                <div class="chevron"></div>
                                <div class="chevron"></div>
                                <div class="chevron"></div>
                            </span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style>
.is-typed span.cursor {
    display: inline-block;
    width: 3px;
    background-color: var(--tp-common-white);
    animation: blink 1s infinite;
}

.is-typed span.cursor.typing {
    animation: none;
}

@keyframes blink {
    49% {
        background-color: var(--tp-common-black);
    }

    50% {
        background-color: transparent;
    }

    99% {
        background-color: transparent;
    }
}

.wave {
    animation-name: wave-animation;
    animation-duration: 2.5s;
    animation-iteration-count: infinite;
    transform-origin: 70% 70%;
    display: inline-block;
}

@keyframes wave-animation {
    0% {
        transform: rotate(0.0deg)
    }

    10% {
        transform: rotate(14.0deg)
    }

    20% {
        transform: rotate(-8.0deg)
    }

    30% {
        transform: rotate(14.0deg)
    }

    40% {
        transform: rotate(-4.0deg)
    }

    50% {
        transform: rotate(10.0deg)
    }

    60% {
        transform: rotate(0.0deg)
    }

    100% {
        transform: rotate(0.0deg)
    }
}

.confetti-above {
    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 1;
}

/* Scroll */
.chevron {
    position: absolute;
    width: 28px;
    height: 8px;
    opacity: 0;
    transform: scale3d(0.5, 0.5, 0.5);
    animation: move 3s ease-out infinite;
}

.chevron:first-child {
    animation: move 3s ease-out 1s infinite;
}

.chevron:nth-child(2) {
    animation: move 3s ease-out 2s infinite;
}

.chevron:before,
.chevron:after {
    content: ' ';
    position: absolute;
    top: 0;
    height: 100%;
    width: 51%;
    background: var(--tp-common-white);
}

.active-light-mode .chevron:before,
.active-light-mode .chevron:after {
    content: ' ';
    position: absolute;
    top: 0;
    height: 100%;
    width: 51%;
    background: var(--tp-common-black);
}

.chevron:before {
    left: 0;
    transform: skew(0deg, 30deg);
}

.chevron:after {
    right: 0;
    width: 50%;
    transform: skew(0deg, -30deg);
}

@keyframes move {
    25% {
        opacity: 1;

    }

    33% {
        opacity: 1;
        transform: translateY(30px);
    }

    67% {
        opacity: 1;
        transform: translateY(40px);
    }

    100% {
        opacity: 0;
        transform: translateY(55px) scale3d(0.5, 0.5, 0.5);
    }
}
</style>
