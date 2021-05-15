<template>
  <div class="flying-emoji-button-component">
    <button @click="appButtonClicked()" ref="button" class="fly-button">{{emoji}}</button>
    <Background ref="background" />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './Background.vue';
import HelloWorld from './HelloWorld.vue';
import Emoji from './Emoji.vue';

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
export default class FlyingEmojiButton extends Vue {
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
