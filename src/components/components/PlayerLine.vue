<script lang="ts">
import Player from '@/viewmodels/Player';
import AppButton from './AppButton.vue';

export default {
  name: 'PlayerLine',
  props: {
      player: Player,
      curSet: Number,
      isFinished: Boolean,
      playerScore: Function
  },
  components: {
    AppButton
  },
}
</script>

<template>
    <tr>
        <td><AppButton label=">" :onClick="playerScore" :disabled="isFinished" size="S"/></td>
        <td class="player">{{player.name}} :</td>
        <td v-bind:class="{'set': true, 'currentSet': curSet == 0 , 'pastSet': curSet > 0 }">{{player.score[0]}}</td>
        <td v-bind:class="{'set': true, 'currentSet': curSet == 1 , 'pastSet': curSet > 1 }">{{player.score[1]}}</td>
        <td v-bind:class="{'set': true, 'currentSet': curSet == 2 && !isFinished , 'pastSet': curSet > 2 }">{{player.score[2]}}</td>
        <td class="game">{{player.gamePoint}}</td>
    </tr>
</template>

<style scoped>
.player {
    text-align: right;
    padding-right: 5px;
}
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