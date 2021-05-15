<template>
  <div class="svg-anime-background">
    <button @click="move(-100, 0)">←</button>
    <button @click="move(100, 0)">→</button>
    <button @click="move(0, -100)">↑</button>
    <button @click="move(0, 100)">↓</button>
    <button @click="splashTo(0, 0)">0</button>
    <button @click="displayEmojiToggle = !displayEmojiToggle">displayEmoji</button>
    <div class="emoji" :style="emoji_style">
      {{ emoji_laugh }}
    </div>
    <transition name="fade">
    <div v-if="displayEmojiToggle"> {{emoji_laugh}} </div>
    </transition>

    <transition-group name="emojis">
    <div v-for="key in emojiKeys" :key="key">
      {{emojis[key]}}
    </div>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';
import { v4 as uuidv4 } from 'uuid';
import { FlyingEmoji } from '../types/flyingEmoji';

export default class HelloWorld extends Vue {
  transform = {
    x: 0,
    y: 0,
  };

  // eslint-disable-next-line camelcase
  emoji_laugh = '😂';

  // eslint-disable-next-line camelcase
  emoji_style = {
    // eslint-disable-next-line vue/no-parsing-error
    transition: 'transform 0.5s ease',
    // eslint-disable-next-line vue/no-parsing-error
    'will-change': 'transform',
    transform: `translate(${this.transform.x}px, ${this.transform.y}px)`,
  };

  msg!: string;

  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  splashTo(x: number, y: number) {
    this.transform.x = x;
    this.transform.y = y;
    this.emoji_style.transform = `translate(${this.transform.x}px, ${this.transform.y}px)`;
  }

  move(x:number, y:number):void {
    this.splashTo(this.transform.x + x, this.transform.y + y);
  }

  splash(emoji :FlyingEmoji):void {
    this.emoji_laugh = emoji.emoji;
    this.splashTo(emoji.toX, emoji.toY);
  }

  displayEmojiToggle = true;

  displayEmoji():void {
    this.displayEmojiToggle = !this.displayEmojiToggle;
  }

  emojis: {[key:string]: string} = {};

  get emojiKeys(): string[] {
    return Object.keys(this.emojis);
  }

  fly(emoji: FlyingEmoji): void {
    const uuid = uuidv4();
    this.emojis[uuid] = emoji.emoji;
    setTimeout(() => {
      delete this.emojis[uuid];
    }, 1000);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}

.svg-anime-background {
  position: fixed;
  top: 0px;
  left: 0px;
  z-index: -1;
  margin: 0;
  padding: 0;

  width: 100vw;
  height: 100vh;
  background: #eeeeee;
}

.emojis-enter-active, .emojis-leave-active {
  transition: transform .5s;
}
.emojis-enter-from, .emojis-leave-to {
  transform: translate(1000px, 1000px)
}

/*
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
*/
</style>
