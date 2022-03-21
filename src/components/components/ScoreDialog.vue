<script lang="ts">
import AppButton from './AppButton.vue';
import { Options, Vue } from 'vue-class-component';
import Match from '@/viewmodels/Match';
import Player from '@/viewmodels/Player';
import { MatchScore, Score }  from '@/viewmodels/Types';
import 'gitart-vue-dialog/dist/style.css';
import { GDialog } from 'gitart-vue-dialog';

@Options({
  props: {
    match: Match,
    isOpen: Boolean,
    onClose: Function
  },
  components: {
    AppButton,
    GDialog
  },
  methods: {
    setScore() {
      let newScore : MatchScore = {
        playerOneScore: [this.set1Pl1, this.set2Pl1, this.set3Pl1] as Score,
        playerTwoScore: [this.set1Pl2, this.set2Pl2, this.set3Pl2] as Score,
        playerOnePoint: isNaN(parseInt(this.pointPl1)) ? this.pointPl1 : parseInt(this.pointPl1),
        playerTwoPoint: isNaN(parseInt(this.pointPl2)) ? this.pointPl2 : parseInt(this.pointPl2),
      }
      const error = this.match.setScore(newScore);
      if(error.code != 0){
        this.errorMessage = error.message;
      } else {
        this.onClose();
      }
    }
  },
  watch: { 
    isOpen: function(_) { // watch it
      let player1 = ((this.match as Match).getPlayerOne() as Player);
      let player2 = ((this.match as Match).getPlayerTwo() as Player);
      this.set1Pl1 = player1.score[0];
      this.set2Pl1 = player1.score[1];
      this.set3Pl1 = player1.score[2];
      this.set1Pl2 = player2.score[0];
      this.set2Pl2 = player2.score[1];
      this.set3Pl2 = player2.score[2];
      this.pointPl1 = player1.gamePoint;
      this.pointPl2 = player2.gamePoint;
      this.errorMessage = '';
    }
  },
  created() {
    this.LISTSET = [0,1,2,3,4,5,6,7] as Array<number>;
  },
  data(){
    return {
      errorMessage: ''
    }
  }
})

export default class ScoreDialog extends Vue {
}

</script>

<template>
    <GDialog v-model="isOpen" persistent max-width="750" >
      <div class="content">
        <div class="title">Édition du score</div>
        <div>
          <table>
            <thead>
              <tr>
              <td>Joueur</td>
              <td>Premier Set</td>
              <td>Second Set</td>
              <td>Troisième Set</td>
              <td>Point</td></tr>
            </thead>
            <tbody>
              <tr>
                <td><h4>{{match.getPlayerOne().name}}</h4></td>
                <td>
                  <select v-model="set1Pl1">
                    <option v-for="set in LISTSET" :value="set" v-bind:key="set">{{set}}</option>
                  </select>
                </td>
                <td>
                  <select v-model="set2Pl1">
                    <option v-for="set in LISTSET" :value="set" v-bind:key="set">{{set}}</option>
                  </select>
                </td>
                <td>
                  <select v-model="set3Pl1">
                    <option v-for="set in LISTSET" :value="set" v-bind:key="set">{{set}}</option>
                  </select>
                </td>
                <td>
                  <input v-model="pointPl1"/>
                </td>
              </tr>
              <tr>
                <td><h4>{{match.getPlayerTwo().name}}</h4></td>
                <td>
                  <select v-model="set1Pl2">
                    <option v-for="set in LISTSET" :value="set" v-bind:key="set" v-bind:selected="{'selected': set == 1}">{{set}}</option>
                  </select>
                </td>
                <td>
                  <select v-model="set2Pl2">
                    <option v-for="set in LISTSET" :value="set" v-bind:key="set">{{set}}</option>
                  </select>
                </td>
                <td>
                  <select v-model="set3Pl2">
                    <option v-for="set in LISTSET" :value="set" v-bind:key="set">{{set}}</option>
                  </select>
                </td>
                <td>
                  <input v-model="pointPl2"/>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        
        <div class="actions">
          <h5 id="errorMessage">{{errorMessage}}</h5>
          <AppButton label="Valider" :onClick="setScore"/>
          <AppButton label="Annuler" :onClick="onClose"/>
        </div>
      </div>
    </GDialog>
</template>

<style scoped>
input, select {
  width: 50%;
  font-family: 'Montserrat', sans-serif;
  background-color: transparent;
  border: 1px solid black;
  border-radius: 10px;
  color: black;
  padding: 5px;
  margin-left: 5px;
  margin-right: 10px;
  font-weight: bold;
}

table {
  width:100%;
  text-align: center;
}

table td {
  width:20%;
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
  margin-top: 20px;
  padding: 10px 20px;
  border-top: 1px solid rgba(0, 0, 0, 0.12);
}

button {
  margin-left: 10px;
}

#errorMessage {
  font-weight: bold;
  color: red;
  margin:auto;
  margin-right: 20px;
  text-align: right;
}
</style>