<script setup>
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' },
    { name: 'description', content: 'Portfolio of Ndjibu Malu Shammah, Full Stack Developer.' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'fr'
  }
})

const title = 'Ndjibu Malu Shammah | Portfolio'
const description = 'Portfolio professionnel de Ndjibu Malu Shammah, étudiante en Master IMSI et développeuse Full Stack.'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  twitterCard: 'summary_large_image'
})
</script>

<template>
  <UApp>
    <NuxtPage />
  </UApp>
</template>
