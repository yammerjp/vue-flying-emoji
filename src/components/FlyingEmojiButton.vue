<template>
  <div class="flying-emoji-button-component">
    <div class="fly-button-wrapper">
      <button ref="button"
        @click="preventIntervalTooShort()"
        :class="{'fly-button': true, animation: isAnimating}"
      >{{charactor}}</button>
    </div>
   <Background ref="background" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component } from 'vue-property-decorator';
import Background from './Background.vue';
import HelloWorld from './HelloWorld.vue';
import EmojiCell from './EmojiCell.vue';

const { random } = Math;

@Component({
  components: {
    Background,
    HelloWorld,
    EmojiCell,
  },
})
export default class FlyingEmojiButton extends Vue {
    $refs!: {
      button: HTMLButtonElement,
      background: Background,
    };

    private charactor = '❤️'

    private isAnimating = false

    preventIntervalTooShort(): void {
      if (this.isAnimating) {
        return;
      }
      this.isAnimating = true;
      this.fly3times();
      setTimeout(() => {
        this.isAnimating = false;
      }, 300);
    }

    private fly3times(): void {
      const { left, top } = this.$refs.button.getBoundingClientRect();
      this.fly(left, top);
      this.fly(left, top);
      this.fly(left, top);
    }

    private fly(buttonX: number, buttonY: number):void {
      this.$refs.background.fly({
        fromX: buttonX,
        fromY: buttonY,
        toX: random() * document.documentElement.clientWidth,
        toY: random() * document.documentElement.clientHeight,
        emoji: this.charactor,
      });
    }
}

</script>

<style scoped>
.fly-button {
  /* ボタンタグのUserAgentStyleSheetの解除 */
    background-color: transparent;
    border: none;
    cursor: pointer;
    outline: none;
    padding: 0;
    appearance: none;
    margin: 0; /* 絵文字の位置計算に用いるので必ず0 */
    padding: 0; /* 絵文字の位置計算に用いるので必ず0 */
    font-size: 24px;
    user-select: none;
}
.fly-button:hover {
  transform: scale(0.95);
}
.fly-button-wrapper {
    display: inline-block;
    margin: 12px;
    user-select: none;
}
/*
.fly-button:active {
 animation: pressed 0.3s 1 ease-out;
}
*/
.animation {
  animation-direction: normal;
  animation-duration: 0.3s;
  animation-name: pressed;
  animation-timing-function: ease;
}
@keyframes pressed {
  0% {
    transform: scale(0.95);
  }
  20% {
    transform: scale(0.0);
  }
  100% {
    transform: scale(1);
  }
}
</style>
