<script setup>
import {ref} from 'vue'

const currentImage = ref(0)

const props = defineProps({
  items: Array
})

const nextImg = () => {
  currentImage.value = (currentImage.value + 1) % props.items.length;
  console.log(currentImage.value)
}
const prevImg = () => {
  currentImage.value = (currentImage.value - 1 + props.items.length) % props.items.length;
}
</script>
<template>
  <div class="car">
    <div class="carousel-slide" :style="{ transform: `translateX(-${currentImage * 100}%)` }">
      <div class="slide" v-for="(item, index) in items" :key="index">
        <h2 class="text-center">{{ item.title }}</h2>
        <img :src="item.pic" :alt="'Image ' + (index + 1)">
      </div>
    </div>
    
    <div class="arrow left flex-c-c" @click="prevImg">
      <img class="icon-white" src="../assets/al.png" alt="Previous">
    </div>
    <div class="arrow right flex-c-c" @click="nextImg">
      <img class="icon-white" src="../assets/ar.png" alt="Next">
    </div>
  </div>
</template>

<style scoped>
.car,.slide,.carousel-slide{
  height:100%;
}
.car{
  overflow:hidden;
  position:relative;
  width:clamp(350px, 100%, 60rem);
  aspect-ratio: 16/9;
}
.arrow {
  width: 50px;
  aspect-ratio: 1;
  position: absolute;
  top: 50%;
  background-color: black;
  border-radius:50%;
  cursor:pointer;
}
.left{
  left:10px;
}
.right{
  right:10px;
}
.arrow > img{
  width:30px;
  height:30px;
}

.carousel-slide {
  display: flex;
  transition: transform 0.3s ease-in-out;
  
}
.slide {
  min-width:100%;
}
.slide > img {
  width:100%;
  height:100%;
  object-fit: fill;
  max-height:600px;
}
</style>