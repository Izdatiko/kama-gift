<template>
    <swiper
      :slides-per-view="1"
      :space-between="50"
    >
      <swiper-slide>
        <img src="/assets/img1.jpg" alt="">
      </swiper-slide>
      <swiper-slide>
        <img src="/assets/img2.jpg" alt="">

      </swiper-slide>
      <swiper-slide>
        <img src="/assets/img3.jpg" alt="">
      </swiper-slide>
      <swiper-slide>
        <video width="100%" height="360" controls>
          <source src="/assets/1.MP4?url" type="video/mp4">
        </video>
      </swiper-slide>
      <swiper-slide>
        <video width="100%" height="360" controls>
            <source src="/assets/3.MOV?url" type="video/mp4">
          </video>
    </swiper-slide>

    </swiper>
  </template>
  
  <script setup>
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import 'swiper/css';
  
  </script>
  
  <style>
  img {
    max-width: 100%;
    width: 100%;
    height: 500px
  }
  </style>
  