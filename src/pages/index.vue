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
          v-card-text.text-overline.text-center Sketch Blog
        v-card(href="https://comics.3and3.dev" width="400px")
          v-img(src="/comic.png")
          v-card-text.text-overline.text-center Comics
  v-card(variant="outlined")
    v-card-title Speedrunning
    v-card.src-times.mx-2.mb-2.px-2.pb-3(variant="outlined")
      .d-flex.flex-column.game(v-for="([game, runs]) of srcTimes")
        .text-overline.text-truncate.title {{game}}
        .text-caption.entry(v-for="run of runs")
          strong &bull;
          span {{run.catName}}
          em {{run.subCats}}:
          a(:href="run.link") {{run.time}}
          span ({{run.ord}})
    v-card-actions
      link-btn(url="https://twitch.tv/threeandthree" src="/twitch.svg" desc="Twitch.tv")
      link-btn(url="https://youtube.com/@threeandthree" src="/youtube.svg" desc="YouTube")
      link-btn(url="https://www.speedrun.com/users/threeandthree" src="/src.png" desc="Speedrun.com")
      link-btn(url="https://racetime.gg/user/DMLq1oZAge3OeQG8/threeandthree" src="/racetime.svg" desc="Racetime.gg")
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { load } from 'js-yaml'
import projectsYaml from '@/assets/projects.yaml?raw'

const projects = load(projectsYaml)
const srcTimes = ref([])

onMounted(async () => {
  const resp = await fetch('https://src-times.threeandthree.deno.net')
  srcTimes.value = await resp.json()
})
</script>

<style lang="sass">
.src-times
  .game
    margin-top: 20px
    margin-bottom: 4px
    border-left: 1px solid #ccc
    padding: 0 0 0 8px
    .title
      margin-top: -12px
      margin-bottom: -12px
    .entry
      margin-top: 4px
      margin-bottom: -4px
      margin-left: 12px
      text-indent: -8px
      *
        margin-right: 4px
</style>
