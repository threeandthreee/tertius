<template lang="pug">
.mx-8
  h1.mb-8 Shapez Blueprint Library
  .d-flex.align-center
    v-text-field.mr-2(
      label="Label"
      variant="outlined"
      clearable
      density="compact"
      hide-details="auto"
      v-model="createLabelInput"
      @keyup.enter="createOne"
    )
    v-text-field.mr-2(
      label="Paste Here"
      variant="outlined"
      clearable
      density="compact"
      hide-details="auto"
      v-model="createValueInput"
      @keyup.enter="createOne"
    )
    v-btn(
      prepend-icon="mdi-plus-circle-outline"
      color="green"
      @click="createOne"
    ) New Blueprint
  v-card.my-2.pa-2(
    v-for="blueprint, index in blueprints"
    :key="index"
    @click="copyOne(index)"
  )
    .d-flex
      h2 {{blueprint.label}}
      v-spacer
      v-btn(
        v-if="!autosort"
        icon="mdi-arrow-up-bold"
        variant="outlined"
        size="x-small"
        :disabled="index==0"
        @click="moveOneUp(index)"
      )
      v-btn.ml-2(
        v-if="!autosort"
        icon="mdi-arrow-down-bold"
        variant="outlined"
        size="x-small"
        :disabled="index==blueprints.length-1"
        @click="moveOneDown(index)"
      )
      v-btn.ml-2(
        icon="mdi-close"
        color="red"
        variant="outlined"
        size="x-small"
        @click="deleteOne(index)"
      )
  v-divider.mt-8.mb-4
  p.my-4 Click on a blueprint to copy it to your clipboard. This is intended to be used with the <a href="https://mod.io/g/shapez/m/blueprint-strings" target="_blank">blueprint strings</a> mod. This uses browser storage, so how permanent that is is up to your browser settings. You can export to and import from json below though.
  .d-flex.align-center
    v-btn(variant="outlined" @click="exportAll") Export all data to clipboard
    v-btn.ml-2(variant="outlined" @click="importAll") Import
    v-text-field.ml-2(label="Paste here to import" variant="outlined" clearable density="compact" hide-details="auto" v-model="importInput" @keyup.enter="importAll")
  v-switch(
    label="Automatic alphabetic sort"
    color="primary"
    v-model="autosort"
    @change="sortBlueprints();storeAll()"
  )
</template>

<script setup>
import { ref, onMounted } from 'vue'

const STORAGE_KEY = 'tert.us/blueprints'
const blueprints = ref([])
const createLabelInput = ref('')
const createValueInput = ref('')
const importInput = ref('')
const autosort = ref(true)

onMounted(() => {
  document.title='shapez blueprints'
  loadAll()
})

const loadAll = () => {
  const raw = localStorage.getItem(STORAGE_KEY)
  const parsed = JSON.parse(raw)
  if (Array.isArray(parsed?.blueprints)){
    blueprints.value = parsed.blueprints
    autosort.value = parsed.autosort
  }
}

const importAll = () => {
  const parsed = JSON.parse(importInput.value)
  if (Array.isArray(parsed))
    blueprints.value = parsed
  importInput.value = ''
  storeAll()
}

const exportAll = () => {
  const json = JSON.stringify(blueprints.value, null, 2)
  return navigator.clipboard.writeText(json)
}

const storeAll = () => {
  const json = JSON.stringify({
    blueprints: blueprints.value,
    autosort: autosort.value
  })
  localStorage.setItem(STORAGE_KEY, json)
}

const createOne = () => {
  blueprints.value.unshift({
    label: createLabelInput.value || 'untitled',
    value: createValueInput.value
  })
  createLabelInput.value = ''
  createValueInput.value = ''
  sortBlueprints()
  storeAll()
}

const moveOneUp = (index) => {
  const arr = blueprints.value
  ;[arr[index-1], arr[index]] = [arr[index], arr[index-1]]
  storeAll()
}

const moveOneDown = (index) => {
  const arr = blueprints.value
  ;[arr[index], arr[index+1]] = [arr[index+1], arr[index]]
  storeAll()
}

const deleteOne = (index) => {
  if (index < 0 || index >= blueprints.value.length)
    return
  blueprints.value.splice(index, 1)
  storeAll()
}

const copyOne = (index) => {
  const item = blueprints.value[index]
  return navigator.clipboard.writeText(item.value)
}

const sortBlueprints = () => {
  if (!autosort.value)
    return
  blueprints.value.sort((a, b) => a.label.localeCompare(b.label))
}
</script>
