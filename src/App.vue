<template>
  <Background />
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './components/Background.vue';
import HelloWorld from './components/HelloWorld.vue';

@Options({
  components: {
    Background,
    HelloWorld,
  },
})
export default class App extends Vue {}
</script>

<style>
#app {
}
</style>
