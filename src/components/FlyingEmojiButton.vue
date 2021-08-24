<template>
  <div class="flying-emoji-button-component">
    <div class="fly-button-wrapper">
      <button ref="button"
        @click="preventIntervalTooShort($event.target)"
        :class="{'fly-button': true, animation: isAnimation}"
      >{{charactor}}</button>
    </div>
   <Background ref="background" />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Background from './Background.vue';
import HelloWorld from './HelloWorld.vue';
import EmojiCell from './EmojiCell.vue';

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
      button: HTMLButtonElement,
      background: Background,
    };

    $event!: {
      target: HTMLElement,
    };

    private rootNodeWidth = 0;

    private rootNodeHeight = 0;

    private charactor = '❤️'

    private isAnimation = false

    preventIntervalTooShort(ref: HTMLElement): void {
      if (this.isAnimation) {
        return;
      }
      this.fly3times(ref);
      this.isAnimation = true;
      setTimeout(() => {
        this.isAnimation = false;
      }, 300);
    }

    private fly3times(ref: HTMLElement): void {
      console.log(typeof ref);
      // const {left, top} = ref.getBoundingClientRect();
      const { left, top } = this.$refs.button.getBoundingClientRect();
      this.fly(left, top);
      this.fly(left, top);
      this.fly(left, top);
    }

    private fly(buttonX: number, buttonY: number):void {
      this.$refs.background.fly({
        fromX: buttonX,
        fromY: buttonY,
        toX: random() * this.rootNodeWidth,
        toY: random() * this.rootNodeHeight,
        emoji: this.charactor,
      });
    }

    mounted():void {
      const updateRootNodeWidthAndHeight = () => {
        const rootNode = document.documentElement;
        this.rootNodeWidth = rootNode.clientWidth;
        this.rootNodeHeight = rootNode.clientHeight;
        // console.log(`width: ${this.width}, height: ${this.height}`);
      };
      updateRootNodeWidthAndHeight();
      window.addEventListener('resize', updateRootNodeWidthAndHeight);
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
