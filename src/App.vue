<template>
  <div>
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  <span style="color: #eeeeee">__________________________________</span>
  <FlyingEmojiButton emoji="😂"/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import FlyingEmojiButton from './components/FlyingEmojiButton.vue';

@Component({
  components: {
    HelloWorld,
    FlyingEmojiButton,
  },
})

export default class App extends Vue {
}
</script>

<style>
/*
#app {
}
*/
html {
  touch-action: manipulation
}
</style>
