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
const arr = ["Portfolio", "Showcase", "Information", "Blog"];
</script>

<template>
    <SliderSkeleton v-if="loading" />
    <section v-if="!loading" class="slider__area pt-40 pb-70 p-relative slider__height-3 d-flex align-items-center">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-xxl-10">
                    <div class="slider__content-3">
                        <div class="slider__search text-center">
                            <span>
                                <span class="wave">👋</span> Hello, My Name Is <button @click="explode">Ilham</button>
                                <ConfettiExplosion stageHeight="450" stageWidth="400" v-if="visible" :colors="colors" class="confetti-above" />
                            </span>
                            <h3 class="slider__title-3">
                                <vue-writer :array="arr" :eraseSpeed="50" :typeSpeed="100" :delay="1000">
                                    {{ trans("Welcome to My ") }}
                                </vue-writer>
                            </h3>

                            <div class="product__details-info-btn">
                                <Link :href="route('about')" class="tp-btn-border header-button">
                                {{ trans("About") }}
                                </Link>
                                <Link :href="route('prompt.index')" class="tp-btn-border">
                                {{ trans("Download CV") }}
                                </Link>
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
</style>
