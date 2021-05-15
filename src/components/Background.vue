<template>
  <div class="svg-anime-background">
    <div v-for="key of emojiKeys" :key="key">
      <Emoji :flyingEmoji="emojis[key]" :duration="durationMS/1000"/>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import { v4 as uuidv4 } from 'uuid';
import { FlyingEmoji } from '../types/flyingEmoji';
import Emoji from './Emoji.vue';

@Options({
  components: {
    Emoji,
  },
})
export default class HelloWorld extends Vue {
  private durationMS = 1000;

  emojis: {[key:string]: FlyingEmoji} = {};

  get emojiKeys(): string[] {
    return Object.keys(this.emojis);
  }

  fly(emoji: FlyingEmoji): void {
    const uuid = uuidv4();
    this.emojis[uuid] = emoji;
    // setInterval を使って複数の絵文字のタイマーを共通化すると軽量化できるのでは？
    setTimeout(() => {
      delete this.emojis[uuid];
    }, this.durationMS);
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

.emoji-enter-active, .emoji-leave-active {
  transition: transform .5s;
}
.emoji-enter-from, .emoji-leave-to {
  transform: translate(1000px, 0px)
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
