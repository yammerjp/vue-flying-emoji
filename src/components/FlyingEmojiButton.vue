<template>
  <div class="flying-emoji-button-component">
    <div v-for="(b, idx) of emojiButtons" :key="idx" class="fly-button-wrapper">
      <button
        @click="flyWithRefs(idx, $event.target)"
        :class="{'fly-button': true, animation: b.isAnimation}"
      >{{b.str}}</button>
    </div>
    <div class="fly-button-wrapper">
      <button @click="flyFromLeftTop">fly</button>
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
  '🔥',
  '🍤',
  '🎉',
  '🤩',
];

const randomEmojiStr = ():string => emojiList[Math.floor(random() * emojiList.length)];

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
    };

    $event!: {
      target: HTMLElement,
    };

    private rootNodeWidth = 0;

    private rootNodeHeight = 0;

    private emojiButtons: {
      str: string;
      isAnimation: boolean;
    }[] = [
      { str: '😇', isAnimation: false },
      { str: '❤️', isAnimation: false },
      { str: '👍', isAnimation: false },
    ];

    flyWithRefs(idx: number, ref: HTMLElement):void {
      // 負荷を未然に防止するためにボタンを押せなくしてみる
      if (this.emojiButtons[idx].isAnimation === true) {
        return;
      }

      this.emojiButtons[idx].isAnimation = true;
      const clientRect = ref.getBoundingClientRect();
      this.flyWithEmojiStr(this.emojiButtons[idx].str, clientRect.left, clientRect.top);
      if (idx === 0) {
        this.emojiButtons[idx].str = randomEmojiStr();
      }
      setTimeout(() => { this.emojiButtons[idx].isAnimation = false; }, 300);
    }

    flyFromLeftTop():void {
      this.flyWithEmojiStr(randomEmojiStr(), this.rootNodeWidth, 0);
    }

    private flyWithEmojiStr(emojiStr: string, buttonX: number, buttonY: number):void {
      for (let i = 0; i < 3; i += 1) {
        this.$refs.background.fly({
          fromX: buttonX,
          fromY: buttonY,
          toX: random() * this.rootNodeWidth,
          toY: random() * this.rootNodeHeight,
          emoji: emojiStr,
        });
      }
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
