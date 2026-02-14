<template lang="pug">
.mx-auto(style="max-width:600px")
  h1.text-h1.d-flex.justify-center
    span tert
    span.pt-12.px-1 i
    span us
  .mx-5.mb-4.d-flex.align-center.justify-space-between
    .d-flex.align-center.mb-1
      div.d-flex.align-center.mr-2(
        style="width:30px;height:30px;background-color:white;border-radius:100%"
      )
        v-img.mx-1(src="/discord.svg")
      p : threeandthree
    .d-flex.align-center.mb-1
      div.d-flex.align-center.mr-2(
        style="width:30px;height:30px;background-color:white;border-radius:100%"
      )
        v-img.mx-1(src="/email.svg")
      p : 3@tert.us
  v-card.mb-4(variant="outlined")
    v-card-title Projects
    v-card-text(v-html="projectsHtml")
    v-card-actions
      link-btn(url="https://github.com/threeandthreee" src="/github.svg" desc="Github")
      link-btn(url="https://codepen.io/alnordst" src="/codepen.svg" desc="Codepen")
  v-card.mb-4(variant="outlined")
    v-card-title Art
    v-card-text
      .d-flex
        v-card.mr-4(href="https://blog.3and3.dev" width="200px")
          v-img(src="/sketch.png")
          v-card-text.text-overline.text-center Doodles
        v-card.mr-4(href="https://comics.3and3.dev" width="200px")
          v-img(src="/comic.png")
          v-card-text.text-overline.text-center Comics
        v-card(href="https://games.3and3.dev" width="200px")
          v-img(src="/game.png")
          v-card-text.text-overline.text-center Games
  v-card(variant="outlined")
    v-card-title Speedrunning
    v-card-actions
      link-btn(url="https://twitch.tv/threeandthree" src="/twitch.svg" desc="Twitch.tv")
      link-btn(url="https://youtube.com/@threeandthree" src="/youtube.svg" desc="YouTube")
      link-btn(url="https://www.speedrun.com/users/threeandthree" src="/src.png" desc="Speedrun.com")
      link-btn(url="https://racetime.gg/user/DMLq1oZAge3OeQG8/threeandthree" src="/racetime.svg" desc="Racetime.gg")
</template>

<script setup>
import { marked } from 'marked'
import projectsMd from '@/assets/projects.md?raw'

const projectsHtml = marked(projectsMd)
</script>
