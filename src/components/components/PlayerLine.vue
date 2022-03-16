<script lang="ts">
import Player from '@/viewmodels/Player'

export default {
  name: 'PlayerLine',
  props: {
      player: Player,
      curSet: Number,
      isFinished: Boolean
  }
}
</script>

<template>
    <tr>
        <td class="player">{{player.name}} :</td>
        <td class="set "
            :class="curSet == 0 ? 'currentSet' : curSet > 0 ? 'pastSet' : ''">{{player.score[0]}}</td>
        <td class="set "
            :class="curSet == 1 ? 'currentSet' : curSet > 1 ? 'pastSet' : ''">{{player.score[1]}}</td>
        <td class="set "
            :class="curSet == 2 ? (isFinished ? '' : 'currentSet') : curSet > 2 ? 'pastSet' : ''">{{player.score[2]}}</td>
        <td class="game">{{player.gamePoint}}</td>
    </tr>
</template>

<style scoped>
.set{
    padding-left: 5px;
    padding-right: 5px;
    border-right:2px solid grey;
}
.game{
    padding-left: 5px;
    padding-right: 5px;
}
.currentSet {
    background: darkorange;
    color: white;
}
.pastSet {
    background: darkgreen;
    color: white;
}
</style>