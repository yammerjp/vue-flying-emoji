<template>
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  <span style="color: #eeeeee">__________________________________</span>
  <button @click="appButtonClicked()" ref="button" class="fly-button">{{emoji}}</button>
  <Background ref="background" />
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './components/Background.vue';
import HelloWorld from './components/HelloWorld.vue';
import Emoji from './components/Emoji.vue';

const emojiList = [
  '😇',
  '🤣',
  '😎',
  '😭',
  '🤔',
  '😂',
  '😈',
  '🤖',
  '👋',
  '👩‍🦰',
];

const { random } = Math;

@Options({
  components: {
    Background,
    HelloWorld,
    Emoji,
  },
})

export default class App extends Vue {
    $refs!: {
      background: Background,
      button: HTMLElement,
    };

    emoji = emojiList[0];

    appButtonClicked():void {
      const clientRect = this.$refs.button.getBoundingClientRect();

      for (let i = 0; i < 50; i += 1) {
        this.$refs.background.fly({
          fromX: clientRect.left,
          fromY: clientRect.top,
          toX: random() * this.width,
          toY: random() * this.height,
          emoji: this.emoji,
        });
      }
      this.emoji = emojiList[Math.floor(random() * emojiList.length)];
    }

    height = 0;

    width = 0;

    mounted():void {
      const updateWidthAndHeight = () => {
        const rootNode = document.documentElement;
        this.width = rootNode.clientWidth;
        this.height = rootNode.clientHeight;
        console.log(`width: ${this.width}, height: ${this.height}`);
      };
      updateWidthAndHeight();
      window.addEventListener('resize', updateWidthAndHeight);
    }
}
</script>

<style>
/*
#app {
}
*/
.fly-button {
    background-color: transparent;
    border: none;
    cursor: pointer;
    outline: none;
    padding: 0;
    appearance: none;
    margin: 0;
    padding: 0;
    font-size: 24px;
}
</style>
