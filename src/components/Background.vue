<template>
  <div class="svg-anime-background">
    <div v-for="key of emojiKeys" :key="key">
      <EmojiCell :flyingEmoji="flyingEmojis[key]" :duration="durationMS/1000"/>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import { v4 as uuidv4 } from 'uuid';
import { FlyingEmojiType } from '../types/flyingEmojiType';
import EmojiCell from './EmojiCell.vue';

@Options({
  components: {
    EmojiCell,
  },
})
export default class Background extends Vue {
  private durationMS = 500;

  flyingEmojis: {[key:string]: FlyingEmojiType} = {};

  get emojiKeys(): string[] {
    return Object.keys(this.flyingEmojis);
  }

  fly(emoji: FlyingEmojiType): void {
    if ((this.deleteMap[this.timeNow])?.length > 100) {
      return;
    }
    const uuid = uuidv4();
    this.flyingEmojis[uuid] = emoji;
    // setInterval を使って複数の絵文字のタイマーを共通化すると軽量化できるのでは？

    if ((this.deleteMap[this.timeNow])?.length > 0) {
      this.deleteMap[this.timeNow].push(uuid);
    } else {
      this.deleteMap[this.timeNow] = [uuid];
    }
  }

  timeNow = 0; // 0 - 50ms * 500ms = 10;

  deleteMap: {[key:number]: string[]} = {
    0: [],
    1: [],
    2: [],
    3: [],
    4: [],
    5: [],
    6: [],
    7: [],
    8: [],
    9: [],
  };

  deleteInterval():void {
    this.timeNow = (this.timeNow + 1) % 10;
    this.deleteMap[this.timeNow].forEach((deleteKey) => {
      delete this.flyingEmojis[deleteKey];
    });
    this.deleteMap[this.timeNow] = [];
  }

  mounted():void {
    console.log(this);
    setInterval(this.deleteInterval, this.durationMS / 10);
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
