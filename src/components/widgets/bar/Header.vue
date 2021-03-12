<template>
  <v-app-bar
    color="transparent"
    flat>
    <img 
      src="@/assets/logo.png"
      width="45"
    />
    <span class="title">Geoguesser</span>
    <div class="flex-grow-1"></div>
    <v-btn 
      text
      color="#FFFFFF"
      href="#section-about">
      <span>ABOUT</span>
    </v-btn>
  </v-app-bar>
</template>

<script lang="ts">
import { defineComponent, } from '@vue/composition-api'

export default defineComponent({

})
</script>

<style scoped>
span {
  color: #FFFFFF;
}

.title {
  font-weight: 700;
}
</style>
