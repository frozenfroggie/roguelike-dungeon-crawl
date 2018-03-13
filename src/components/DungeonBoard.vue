<template>
  <div class="dungeonBoard">
    <the-heading> Dungeon Crawler Game </the-heading>
    <dungeon-board-map></dungeon-board-map>
    <player-panel></player-panel>
  </div>
</template>

<script>
  import TheHeading from './TheHeading.vue';
  import PlayerPanel from './PlayerPanel.vue';
  import DungeonBoardMap from './DungeonBoardMap.vue';

  export default {
    components: {
      TheHeading,
      PlayerPanel,
      DungeonBoardMap
    }
  }
</script>

<style>
  .dungeonBoard {
    width: 86%;
    height: 80%;
    background-color: rgba(0,0,0,0.9);
    border-radius: 5px;
    box-shadow: 1px 1px 30px 0px rgba(193,230,230,0.3);
  }
</style>
