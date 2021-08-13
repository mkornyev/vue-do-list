<template>
  <div class="header">
    
    <h1 class="header">{{ header }}</h1>
    <p class="tagline" v-for="tagline in taglines" v-bind:key="tagline">{{ tagline }}</p>

    <hr/>

  </div>
</template>

<script lang="ts">
  import { defineComponent } from 'vue';

  export default defineComponent({
    name: 'NavHeader',
    props: {
      header: String,
      taglines: {
        type: Array,
        default: () => [String],
      },
    },
  });
</script>

<style scoped>
  h1.header {
    font-size: 3em;
    margin-left: 10%;
    margin-right: 10%;
  }

  p.tagline {
    font-size: 1.5em;
  }

  hr {
    margin-left: 10%;
    margin-right: 10%;
    margin-bottom: 5%;
  }
</style>
