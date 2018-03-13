<template>
  <div class="dungeonBoardHeader">
    <img class="titleIcon" src="../assets/swords.png" />
    <h1 class="dungeonBoardTitle"><slot></slot></h1>
    <img class="titleIcon" src="../assets/helm.png" />
  </div>
</template>

<style scoped>
  .dungeonBoardHeader {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
  }
  .dungeonBoardTitle {
    text-align: center;
    --textBorderFL: rgb(15,15,15);
    --textBorderSL: #202422;
    color: #DEA543;
    text-shadow:
        /* first layer at 1px */
        -1px -1px 0px var(--textBorderFL),
         0px -1px 0px var(--textBorderFL),
         1px -1px 0px var(--textBorderFL),
        -1px  0px 0px var(--textBorderFL),
         1px  0px 0px var(--textBorderFL),
        -1px  1px 0px var(--textBorderFL),
         0px  1px 0px var(--textBorderFL),
         1px  1px 0px var(--textBorderFL),
        /* second layer at 2px */
        -2px -2px 0px var(--textBorderSL),
        -1px -2px 0px var(--textBorderSL),
         0px -2px 0px var(--textBorderSL),
         1px -2px 0px var(--textBorderSL),
         2px -2px 0px var(--textBorderSL),
         2px -1px 0px var(--textBorderSL),
         2px  0px 0px var(--textBorderSL),
         2px  1px 0px var(--textBorderSL),
         2px  2px 0px var(--textBorderSL),
         1px  2px 0px var(--textBorderSL),
         0px  2px 0px var(--textBorderSL),
        -1px  2px 0px var(--textBorderSL),
        -2px  2px 0px var(--textBorderSL),
        -2px  1px 0px var(--textBorderSL),
        -2px  0px 0px var(--textBorderSL),
        -2px -1px 0px var(--textBorderSL);
    letter-spacing: 1.5px;
  }
  .titleIcon {
    width: 50px;
    height: 50px;
  }
</style>
