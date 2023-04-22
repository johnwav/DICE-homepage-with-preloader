<script setup>
import { ref, onMounted, watch } from 'vue'
const images = [
  "https://dice-media.imgix.net/homepage/hero-1.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-2.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-3.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-4.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-5.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-6.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-7.jpg?auto=format,compress",
  "https://dice-media.imgix.net/homepage/hero-8.jpg?auto=format,compress"
]

const imageCount = ref(0)
const loaded = ref(false)

let imageInterval = null

const preloadImages = () => {
  for (let i = 0; i < images.length; i++) {
    const img = new Image();
    img.src = images[i];
  }
};

preloadImages()

onMounted(() => {
  imageInterval = setInterval(() => {
    imageCount.value++
  }, 2500)
})

watch(imageCount, () => {
  if (imageCount.value + 1 === images.length) {
    clearInterval(imageInterval)
  }
})

</script>

<template>
  <section>
    <div>
      <img rel="preload" v-for="(image, index) in images" :src="image"
        :style="imageCount == index ? 'opacity: 1' : 'opacity: 0'" />
    </div>
    <div class="hero-text">
      <h1 class="text">MORE OF THE <br>
        SHOWS YOU LOVE
        <div style="background-image: url(https://media.tenor.com/-r1FcJGxGFMAAAAC/loading-bar.gif);"></div>

      </h1>
    </div>

  </section>
</template>


<style scoped>
section {
  position: relative;
}

section div img {
  height: 100vh;
  width: 100vw;
  object-fit: cover;
  position: absolute;
  transition: opacity 0.5s ease-in-out 0s;
}


section .hero-text {
  position: absolute;
  z-index: 999999;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}


.text {
  text-align: center;
  color: white;
  font-size: clamp(82px, 10vw, 132px);
  font-weight: 800;
  letter-spacing: -0.9vw;
  line-height: clamp(70px, 8vw, 110px);
}

@keyframes opacity {

  0% {
    opacity: 0;
  }

  25% {
    opacity: 0.25;
  }

  50% {
    opacity: 0.5;
  }

  100% {
    opacity: 1;
  }

}
</style>