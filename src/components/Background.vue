<template>
  <div class="svg-anime-background">
    <button @click="move(-100, 0)">←</button>
    <button @click="move(100, 0)">→</button>
    <button @click="move(0, -100)">↑</button>
    <button @click="move(0, 100)">↓</button>
    <button @click="splashTo(0, 0)">s</button>
    <div class="emoji" :style="emoji_style">
      {{emoji_laugh}}
    </div>
  </div>
</template>

<script lang="ts">
import { /* Options, */ Vue } from 'vue-class-component';
/*
@Options({
  props: {
    msg: String,
  },
})
*/

// const wait = (t: number) => new Promise((resolve) => setTimeout(resolve, t));
export default class HelloWorld extends Vue {
  private transform = {
    x: 0,
    y: 0,
  };

  // eslint-disable-next-line camelcase
  private emoji_laugh = '😂';

  // eslint-disable-next-line camelcase
  private emoji_style = {
    // eslint-disable-next-line vue/no-parsing-error
    transition: 'transform 0.5s ease',
    // eslint-disable-next-line vue/no-parsing-error
    'will-change': 'transform',
    transform: `translate(${this.transform.x}px, ${this.transform.y}px)`,
  };

  /*
  msg!: string
  */
  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  move(x: number, y:number) {
    this.transform.x += x;
    this.transform.y += y;
    this.emoji_style.transform = `translate(${this.transform.x}px, ${this.transform.y}px)`;
    console.log(this.transform);
    console.log('clicked');
  }

  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  splashTo(x:number, y:number) {
    this.transform.x = x;
    this.transform.y = y;
    this.emoji_style.transform = `translate(${this.transform.x}px, ${this.transform.y}px)`;
  }
  /*
  data() {
    console.log(this);
  */
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
</style>
