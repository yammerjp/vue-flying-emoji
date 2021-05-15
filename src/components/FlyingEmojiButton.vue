<template>
  <div class="flying-emoji-button-component">
    <div class="fly-button-wrapper">
    <button @click="flyRandom()" ref="flyRandomButton" class="fly-button">{{emojiStr}}</button>
    </div>
    <div class="fly-button-wrapper">
    <button @click="flyPartyPopper()" ref="flyPartyPopperButton" class="fly-button">🎉</button>
    </div>
    <div class="fly-button-wrapper">
    <button @click="flyStarFace()" ref="flyStarFaceButton" class="fly-button">🤩</button>
    </div>
    <Background ref="background" />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './Background.vue';
import HelloWorld from './HelloWorld.vue';
import EmojiCell from './EmojiCell.vue';

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
    EmojiCell,
  },
})
export default class FlyingEmojiButton extends Vue {
    $refs!: {
      background: Background,
      flyRandomButton: HTMLElement,
      flyPartyPopperButton: HTMLElement,
      flyStarFaceButton: HTMLElement,
    };

    height = 0;

    width = 0;

    emojiStr = emojiList[0];

    flyRandom():void {
      const clientRect = this.$refs.flyRandomButton.getBoundingClientRect();
      this.flyWithEmojiStr(this.emojiStr, clientRect.left, clientRect.top);
      this.emojiStr = emojiList[Math.floor(random() * emojiList.length)];
    }

    flyPartyPopper():void {
      const clientRect = this.$refs.flyPartyPopperButton.getBoundingClientRect();
      this.flyWithEmojiStr('🎉', clientRect.left, clientRect.top);
    }

    flyStarFace():void {
      const clientRect = this.$refs.flyStarFaceButton.getBoundingClientRect();
      this.flyWithEmojiStr('🤩', clientRect.left, clientRect.top);
    }

    flyWithEmojiStr(emojiStr: string, buttonX: number, buttonY: number):void {
      for (let i = 0; i < 3; i += 1) {
        this.$refs.background.fly({
          fromX: buttonX,
          fromY: buttonY,
          toX: random() * this.width,
          toY: random() * this.height,
          emoji: emojiStr,
        });
      }
    }

    mounted():void {
      const updateWidthAndHeight = () => {
        const rootNode = document.documentElement;
        this.width = rootNode.clientWidth;
        this.height = rootNode.clientHeight;
        // console.log(`width: ${this.width}, height: ${this.height}`);
      };
      updateWidthAndHeight();
      window.addEventListener('resize', updateWidthAndHeight);
    }
}

</script>

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
.fly-button-wrapper {
    display: inline-block;
    margin: 12px;
}
</style>
