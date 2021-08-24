<template>
  <div class="svg-anime-background">
    <div v-for="key of emojiKeys" :key="key">
      <EmojiCell :flyingEmoji="flyingEmojis[key]" :duration="durationMS/1000"/>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component } from 'vue-property-decorator';
import { v4 as uuidv4 } from 'uuid';
import { FlyingEmojiType } from '../types/flyingEmojiType';
import EmojiCell from './EmojiCell.vue';

@Component({
  components: {
    EmojiCell,
  },
})
export default class Background extends Vue {
  private durationMS = 3000;

  flyingEmojis: {[key:string]: FlyingEmojiType} = {};

  get emojiKeys(): string[] {
    return Object.keys(this.flyingEmojis);
  }

  fly(emoji: FlyingEmojiType): void {
    if ((this.deleteMap[this.timeNow])?.length > 100) {
      return;
    }
    const uuid = uuidv4();
    this.$set(this.flyingEmojis, uuid, emoji);
    // this.flyingEmojis[uuid] = emoji;
    // setInterval を使って複数の絵文字のタイマーを共通化すると軽量化できるのでは？

    if ((this.deleteMap[this.timeNow])?.length > 0) {
      this.deleteMap[this.timeNow].push(uuid);
    } else {
      this.deleteMap[this.timeNow] = [uuid];
    }
  }

  timeNow = 0; // 0-9 // loop counter with setInterval();

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
    setInterval(this.deleteInterval, this.durationMS / 10);
  }
}
</script>

<style scoped>
.svg-anime-background {
  position: fixed;
  top: 0px;
  left: 0px;
  z-index: -1;
  margin: 0;
  padding: 0;
}
</style>
