<template>
    <div>
        <Swiper />
        <p>{{ text }}</p>
    </div>
</template>

<script setup>
import Swiper from "@/components/Swiper.vue";
import axios from "axios";
import { ref, onMounted, onBeforeUnmount } from "vue";

const text = ref('');

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


