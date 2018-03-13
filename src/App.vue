<template>
  <div class='container'>
    <dungeon-board></dungeon-board>
    <the-footer></the-footer>
  </div>
</template>

<script>
import DungeonBoard from './components/DungeonBoard.vue';
import TheFooter from './components/TheFooter.vue';

export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    DungeonBoard,
    TheFooter
  }
}
</script>

<style scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0px;
    bottom: 0px;
    left: 0px;
    right: 0px;
    background-image: url('https://pre00.deviantart.net/1cf6/th/pre/f/2012/021/c/1/c14fbb07fc936cb4ad23d0bdaf5e0079-d4n4zuk.jpg');
    background-size: contain;
  }
</style>
