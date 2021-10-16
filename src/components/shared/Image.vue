<template>
  <div :class="classes" :style="{backgroundImage: 'url('+img+')'}"/>
</template>

<script>
export default {
  name: "Image",
  props: {
    img: String,
    classes: String,
  }
};
</script>

<style scoped>

  div {
    position: relative;
    display: inline-block;
    background: var(--solid);
    background-size: cover;
    background-position: center center;
  }

  div:after {
    position: absolute;
    content: '';
    width: inherit;
    height: inherit;
    background: inherit;
    border-radius: inherit;
    filter: blur(1.25em);
    z-index: -1;
    opacity: .75;
  }
</style>



