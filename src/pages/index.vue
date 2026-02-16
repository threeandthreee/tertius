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
    .mx-4.my-2(v-for="projectGroup, heading of projects")
      h6.text-h6 {{heading}}
      .d-flex.flex-wrap
        v-chip.ma-1.flex-shrink-0(
          v-for="url, label of projectGroup"
          :href="url"
          variant="outlined"
          style="border-radius: 5px"
        ) {{label}}
    v-card-actions
      link-btn(url="https://github.com/threeandthreee" src="/github.svg" desc="Github")
      link-btn(url="https://codepen.io/alnordst" src="/codepen.svg" desc="Codepen")
  v-card.mb-4(variant="outlined")
    v-card-title Art
    v-card-text
      .d-flex
        v-card.mr-4(href="https://blog.3and3.dev" width="400px")
          v-img(src="/sketch.png")
          v-card-text.text-overline.text-center Doodles
        v-card.mr-4(href="https://comics.3and3.dev" width="400px")
          v-img(src="/comic.png")
          v-card-text.text-overline.text-center Comics
  v-card(variant="outlined")
    v-card-title Speedrunning
    v-card-actions
      link-btn(url="https://twitch.tv/threeandthree" src="/twitch.svg" desc="Twitch.tv")
      link-btn(url="https://youtube.com/@threeandthree" src="/youtube.svg" desc="YouTube")
      link-btn(url="https://www.speedrun.com/users/threeandthree" src="/src.png" desc="Speedrun.com")
      link-btn(url="https://racetime.gg/user/DMLq1oZAge3OeQG8/threeandthree" src="/racetime.svg" desc="Racetime.gg")
</template>

<script setup>
import { load } from 'js-yaml'
import projectsYaml from '@/assets/projects.yaml?raw'

const projects = load(projectsYaml)

/*
const projects = [
  {
    url: 'https://raceswild.3and3.dev',
    label: 'Races Wild',
  },
  {
    url: 'https://github.com/threeandthreee/archipelago',
    label: "Link's Awakening DX for Archipelago"
  },
  {
    url: 'https://vod-sync.3and3.dev',
    label: 'Vod Sync'
  },
  {
    url: 'https://la-menu.3and3.dev',
    label: 'LA/DX Menu Router'
  },
  {
    url: '/blueprints',
    label: 'Shapez Blueprint Library'
  },
  {
    url: 'https://ladx-gfx.3and3.dev/',
    label: 'LADX Custom Sprite Tools'
  }
]
projects.sort((a, b) => a.label.localeCompare(b.label))
*/
</script>
