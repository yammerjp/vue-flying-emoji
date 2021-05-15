<template>
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  <span style="color: #eeeeee">__________________________________</span>
  <FlyingEmojiButton/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HelloWorld from './components/HelloWorld.vue';
import FlyingEmojiButton from './components/FlyingEmojiButton.vue';

@Options({
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
