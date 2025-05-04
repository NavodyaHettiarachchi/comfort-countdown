<template>
  <div class="container">
    <div class="top-row">
      <img class="logo" src="/logo.png" alt="Comfort logo" />
    </div>

    <div class="main-content">
      <h1>Testing phase closed.</h1>
      <h2>Official launch on May 8th.</h2>
      <p>We’ve always been about Comfort. Now with a smart new bot to help you, anytime you need.</p>

      <div class="countdown-row">
        <!-- Left badge -->
        <div class="badge loved">
          <p>Most Loved Household Brand 2023</p>
          <a href="https://brandfinance.com" target="_blank">Brand Finance</a>
        </div>

        <!-- Countdown -->
        <div class="countdown">
          <div><span>{{ countdown.days }}</span><span class="label">days</span></div>
          <div><span>{{ countdown.hours }}</span><span class="label">hours</span></div>
          <div><span>{{ countdown.minutes }}</span><span class="label">min</span></div>
          <div><span>{{ countdown.seconds }}</span><span class="label">sec</span></div>
        </div>

        <!-- Right badge -->
        <div class="badge trusted">
          <p>Trusted by</p>
          <p><strong>millions of households</strong></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const countdown = ref({
  days: '00',
  hours: '00',
  minutes: '00',
  seconds: '00'
})

const targetDate = new Date('2025-05-08T00:00:00')

function updateCountdown() {
  const now = new Date()
  const diff = targetDate - now

  if (diff <= 0) {
    countdown.value = { days: '00', hours: '00', minutes: '00', seconds: '00' }
    return
  }

  const seconds = Math.floor((diff / 1000) % 60)
  const minutes = Math.floor((diff / 1000 / 60) % 60)
  const hours = Math.floor((diff / 1000 / 60 / 60) % 24)
  const days = Math.floor(diff / (1000 * 60 * 60 * 24))

  countdown.value = {
    days: String(days).padStart(2, '0'),
    hours: String(hours).padStart(2, '0'),
    minutes: String(minutes).padStart(2, '0'),
    seconds: String(seconds).padStart(2, '0')
  }
}

let interval

onMounted(() => {
  updateCountdown()
  interval = setInterval(updateCountdown, 1000)
})

onBeforeUnmount(() => {
  clearInterval(interval)
})
</script>
