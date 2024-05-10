<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue';
import IconFacebook from './assets/icon-facebook.svg';
import IconInstagram from './assets/icon-instagram.svg';
import IconPinterest from './assets/icon-pinterest.svg';

const countdownDate = new Date();
countdownDate.setDate(countdownDate.getDate() + 14); // Adding 2 days to the current date

const currentTime = ref(new Date());

const days = ref(0);
const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);

const calculateTimeLeft = () => {
  const difference = countdownDate - currentTime.value;

  if (difference > 0) {
    days.value = Math.floor(difference / (1000 * 60 * 60 * 24));
    hours.value = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    minutes.value = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
    seconds.value = Math.floor((difference % (1000 * 60)) / 1000);
  } else {
    days.value = 0;
    hours.value = 0;
    minutes.value = 0;
    seconds.value = 0;
  }
};

const timer = setInterval(() => {
  currentTime.value = new Date();
}, 1000);

onMounted(() => {
  calculateTimeLeft();
});

watch(currentTime, () => {
  calculateTimeLeft();
});

onBeforeUnmount(() => {
  clearInterval(timer);
});

</script>

<template>
    <div class="container">
    <div class="title"><h1>We're launching soon</h1></div>
    <div class="counter">
      <div class="time-card"><h2>{{ days }}</h2></div>
      <h3>days</h3>
      <div class="time-card"><h2>{{ hours }}</h2></div>
      <h3>hours</h3>
      <div class="time-card"><h2>{{ minutes }}</h2></div>
      <h3>minutes</h3>
      <div class="time-card"><h2>{{ seconds }}</h2></div>
      <h3>seconds</h3>
    </div>
    <div class="footer">
      <div class="socials">
      <img class="social-icon" :src="IconFacebook" alt="Icon Facebook"/>
      <img class="social-icon" :src="IconInstagram" alt="Icon Instagram"/>
      <img class="social-icon" :src="IconPinterest" alt="Icon Pinterest"/>
    </div>
    </div>
  </div>
</template>
