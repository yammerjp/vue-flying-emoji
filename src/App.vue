<template>
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  <span style="color: #eeeeee">__________________________________</span>
  <FlyingEmojiButton/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './components/Background.vue';
import HelloWorld from './components/HelloWorld.vue';
import Emoji from './components/Emoji.vue';
import FlyingEmojiButton from './components/FlyingEmojiButton.vue';

@Options({
  components: {
    Background,
    HelloWorld,
    Emoji,
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
</style>
