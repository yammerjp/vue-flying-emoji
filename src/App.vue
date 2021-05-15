<template>
  <br/>
  <br/>
  <button @click="appButtonClicked()">appButton</button>
  <button @click="appButton2Clicked()">appButton2</button>
  <Background ref="background" />
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './components/Background.vue';
import HelloWorld from './components/HelloWorld.vue';

type FlyingEmoji = {
    fromX: number;
    fromY: number;
    toX: number;
    toY: number;
    emoji: string;
};

@Options({
  components: {
    Background,
    HelloWorld,
  },
})
export default class App extends Vue {
    $refs!: {
      background: Background
    };

    flyingEmojis: FlyingEmoji[] = [{
      fromX: 0,
      fromY: 0,
      toX: 1000,
      toY: 1000,
      emoji: '😎',
    },
    {
      fromX: 0,
      fromY: 0,
      toX: 0,
      toY: 0,
      emoji: '😎',
    }];

    appButtonClicked():void {
      this.$refs.background.fly(this.flyingEmojis[0]);
    }

    appButton2Clicked():void {
      this.$refs.background.splash(this.flyingEmojis[1]);
    }
}
</script>

<style>
/*
#app {
}
*/
</style>
