<script lang="ts">
import PlayerLine from './PlayerLine.vue';
import 'gitart-vue-dialog/dist/style.css';
import AppButton from './AppButton.vue';
import ScoreDialog from './ScoreDialog.vue';
import { GDialog } from 'gitart-vue-dialog';
import { Options, Vue } from 'vue-class-component';
import Match from '@/viewmodels/Match';

@Options({
  props: {
    match: Match
  },
  components: {
    PlayerLine,
    AppButton,
    GDialog,
    ScoreDialog
  },
  methods: {
    newPoint(){
      this.nbPoint = this.nbPoint == "" || this.nbPoint < 1 ? 1 : this.nbPoint;
      for(let i = 0; i < this.nbPoint; i++){
        this.match.playPoint();
      }
    },
    playerOneScores(){ this.match.playerOneScores() },
    playerTwoScores(){ this.match.playerTwoScores() },
    openCloseScoreDialog() {
      this.isOpenScoreDialog = !this.isOpenScoreDialog;
    },

  },
  data() {
    return {
      nbPoint: 1,
      isOpenScoreDialog: false
    };
  },
})

export default class MatchBox extends Vue {
  
}

</script>

<template>
  <div class="matchBox">
    <ScoreDialog :match="match" :isOpen="isOpenScoreDialog" :onClose="openCloseScoreDialog"/>
    <AppButton label="Set Score" :onClick="openCloseScoreDialog" :disabled="this.match.getIsFinished()" size="N"/>
    <table>
      <tbody>
          <PlayerLine :playerScore="playerOneScores" :player="this.match.getPlayerOne()" :curSet="this.match.getCurrentSet()" :isFinished="this.match.getIsFinished()"/>
          <PlayerLine :playerScore="playerTwoScores" :player="this.match.getPlayerTwo()" :curSet="this.match.getCurrentSet()" :isFinished="this.match.getIsFinished()"/>
      </tbody>
    </table>
    <input v-model.number="nbPoint" type="number" :disabled="this.match.getIsFinished()"/>
    <AppButton label="Jouer le point" :onClick="newPoint" :disabled="this.match.getIsFinished()"/>
  </div>
</template>

<style scoped>
table {
  margin: 10px
}
.matchBox {
  margin: 10px;
  display:inline-block;
  background-color: transparent;
  border: 2px solid lightgray;
  border-radius: 10px;
  color: black;
  padding: 10px;
  font-weight: bold;
}
input {
  width: 100px;
  font-family: 'Montserrat', sans-serif;
  background-color: transparent;
  border: 2px solid black;
  border-radius: 10px;
  color: black;
  padding: 10px;
  font-weight: bold;
}
input:disabled,
input[disabled]{
  border: 1px solid #a5a5a5;
  color: #a5a5a5;
}


.title {
  font-size: 30px;
  font-weight: 700;
  margin-bottom: 20px;
}

.content {
  padding: 20px;
}

.actions {
  display: flex;
  justify-content: flex-end;
  padding: 10px 20px;
  border-top: 1px solid rgba(0, 0, 0, 0.12);
}
</style>