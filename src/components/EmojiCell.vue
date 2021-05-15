<template>
  <div class="float-background" :style="styleObject">
  <transition name="fade" appear @enter="enter" :css="false">
    <div> {{flyingEmoji.emoji}} </div>
  </transition>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import gsap from 'gsap';
import { FlyingEmojiType } from '../types/flyingEmojiType';

@Options({
  props: {
    flyingEmoji: Object,
    duration: Number,
  },
})

export default class EmojiCell extends Vue {
  flyingEmoji!: FlyingEmojiType;

  duration!: number;

  enter(el: HTMLElement, done: (()=>void)):void {
    gsap.to(el, {
      duration: this.duration,
      x: this.flyingEmoji.toX - this.flyingEmoji.fromX,
      y: this.flyingEmoji.toY - this.flyingEmoji.fromY,
      onComplete: done,
    });
  }

  styleObject = {
    top: `${this.flyingEmoji.fromY}px`,
    left: `${this.flyingEmoji.fromX}px`,
  };
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.float-background {
  position: fixed;
  z-index: -1;
  margin: 0;
  padding: 0;
  font-size: 24px;
}
</style>
