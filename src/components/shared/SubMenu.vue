<template>
  <router-link v-for="({url, icon, text, tooltip}, index) in menus" :tooltip="tooltip" flow="right" :key="index" :style="styles ? styles : undefined" :class="'content-center items-center' + (classes ? ' ' + classes : '')" :to="url">
    <Card contentClasses="p-1" 
      :classes="'clickable items-center content-center text-center' + (currentRoute(url) ? ' active' : '')"
      headerClasses="items-center content-center">
      <span :class="icon"></span>
      <span >{{text}}</span>
    </Card>
  </router-link>
</template>

<script setup>
import Card from "./Card.vue"
import { useRoute } from 'vue-router';

const currentRoute = url => {
  if(useRoute().path == url){
    return true
  } else{
    return false
  }
}

defineProps({
  menus: Array,
  classes: String,
  styles: String
})
  
</script>