<template>
  <div :class="'card' + (classes ? ' ' + classes : '')" :style="style">
    <div v-if="!!this.$slots.header" :class="'card-header' + (headerClasses ? ' ' + headerClasses : '')" :style=headerStyle>
      <slot name="header"/>
    </div>
    <div v-if="!!this.$slots.default" :class="'card-content' + (contentClasses ? ' ' + contentClasses : '')" :style="contentStyle">
      <slot/>
    </div>
  </div>
</template>

<script setup>
defineProps({  
  classes: String, 
  style: String, 
  headerClasses: String, 
  headerStyle: String, 
  contentClasses: String, 
  contentStyle:String
})
</script> 

<style scoped>
  /* ==================== BEGIN CARD ==================== */
  .card {
    position: relative;
    display: flex;
    overflow: auto;
    background: hsla(var(--card-bg-color), 1);
    border-radius: 1.2rem;
    flex-direction: column;
    border: .1rem solid hsla(var(--card-bg-color), .3);
    justify-content: flex-start;
    background-clip: padding-box;

    transition: width 1s ease, height 1s ease;
  }

  .card.active {
    background-color: hsla(var(--primary-bg-color), .8);
  }

  .card.active .card-header {
    background-color: hsla(var(--primary-bg-color), .1);
    /* border-color: hsla(var(--primary-bg-color), .3); */
    color: hsl(var(--primary-text-color));
  }

  .card.active .card-content {
    color: white;
  }

  .card.opaque {
    background: hsl(var(--card-bg-color));
  }

  .card.base {
    background-color: hsla(var(--base-color), var(--opacityDefault));
  }

  .card.outline {
    border-color: hsla(var(--text-color), .3);
  }

  /* VANILLA CARD */

  .card-header {
    display: flex;
    padding: 1rem;
    background: hsla(var(--text-color), .1);
    border: 0;
    color: hsl(var(--text-color));
    background-clip: padding-box;
  }

  /* .card.outline .card-header {
    border-bottom: .1rem solid hsla(var(--text-color), .3);
  } */

  .card-content {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    padding: 2em;
    background: transparent;
    border: 0;
    color: hsl(var(--text-color));
  }

  .card .card-content hr {
    background: hsla(var(--text-color), .5);
  }

  .card.clickable:hover:not(.active) {
    background: hsl(var(--card-bg-color));
    border-color: hsla(var(--primary-bg-color), .85);
    color: hsl(var(--primary-bg-color));
    cursor: pointer;
  }

  .card.clickable:hover:not(.active) .card-content {
    color: hsl(var(--primary-bg-color));
  }
    
  .card.clickable:active:not(.active) {
    background: hsl(var(--card-bg-color));
    border-color: hsla(var(--primary-text-color), 1);
    color: hsl(var(--primary-text-color));
  }

  .card.clickable:active:not(.active) .card-content{
    color: hsl(var(--primary-text-color));
  }

  /* ==================== END CARD ==================== */
</style>
