<template lang="pug">
v-tooltip(bottom)
  template(v-slot:activator="{ on, attrs }")
    v-btn.mt-0.mb-1.mx-1.link-btn(icon :href="url" v-bind="attrs" v-on="on")
      v-img(:src="src" contain height=30 width=30)
  span {{desc}}
</template>

<script>
export default {
  props: ['url', 'src', 'desc']
}
</script>

<style>
.link-btn {
  background-color: white;
}
</style>