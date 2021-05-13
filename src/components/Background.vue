<template>
  <div class="svg-anime-background">
    <div class="emoji">
      {{emoji_laugh}}
    </div>
  </div>
</template>

<script lang="js">
import { /* Options, */ Vue } from 'vue-class-component';
/*
@Options({
  props: {
    msg: String,
  },
})
*/
export default class HelloWorld extends Vue {
  /*
  msg!: string
  */
  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  data() {
    console.log(this);
    return ({
      emoji_laugh: '😂',
    });
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
</style>
