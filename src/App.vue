<template>
  <FlyingEmojiButton :emoji="emoji">
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import FlyingEmojiButton from './components/FlyingEmojiButton.vue';

@Component({
  components: {
    FlyingEmojiButton,
  },
})
export default class App extends Vue {
  @Prop(String) emoji!: string
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
