<template>
    <div>
        <Swiper v-if="isSwiper"/>
        <video width="100%" height="360" controls v-if="isFlex">
            <source src="/assets/flex.MOV?url" type="video/mp4">
          </video>
          <video width="100%" height="360" controls v-if="moreFlex">
            <source src="/assets/flex2.MOV?url" type="video/mp4">
          </video>

        <p>{{ text }}</p>

        <button v-if="isSwiper" @click="show">
            Показать flex
        </button>
        <button @click="showMoreFlex" v-if="!isSwiper">Еще больше flex</button>
    </div>
</template>

<script setup>
import Swiper from "@/components/Swiper.vue";
import axios from "axios";
import { ref, onMounted, onBeforeUnmount } from "vue";

const text = ref('');

const moreFlex = ref(false)

const isFlex = ref(false)

const isSwiper = ref(true);

const show = () => {
    isSwiper.value = false
    isFlex.value = true
}

const showMoreFlex = () => {
    isFlex.value = false
    moreFlex.value = true
}

const getText = async () => {
    try {
        const res = await axios.get("https://tools-api.robolatoriya.com/compliment");
        text.value = res.data.text;
    } catch (error) {
        console.error("Error fetching data:", error);
    }
}

let intervalId;

onMounted(() => {
    getText(); 
    intervalId = setInterval(getText, 3000);
});

onBeforeUnmount(() => {
    clearInterval(intervalId);
});
</script>

<style>
p {
    font-family: "Handjet";
    line-height: 1.2em;
    font-size: 40px;
    text-align: center;
}
</style>


