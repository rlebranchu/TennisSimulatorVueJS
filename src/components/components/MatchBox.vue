<script lang="ts">
import PlayerLine from './PlayerLine.vue';
import AppButton from './AppButton.vue';
import { Options, Vue } from 'vue-class-component';
import Match from '@/viewmodels/Match';

@Options({
  props: {
    match: Match,
    nbPoint: Number,
  },
  components: {
    PlayerLine,
    AppButton
  },
  methods: {
    newPoint(){
      this.nbPoint = this.nbPoint == "" || this.nbPoint < 1 ? 1 : this.nbPoint;
      for(let i = 0; i < this.nbPoint; i++){
        this.match.playPoint();
      }
    }
  },
  data() {
    return {
      nbPoint: 1,
    };
  },
})

export default class MatchBox extends Vue {
  
}

</script>

<template>
  <div class="matchBox">
    <table>
      <tbody>
          <PlayerLine :player="this.match.getPlayerOne()" :curSet="this.match.getCurrentSet()" :isFinished="this.match.getIsFinished()"/>
          <PlayerLine :player="this.match.getPlayerTwo()" :curSet="this.match.getCurrentSet()" :isFinished="this.match.getIsFinished()"/>
      </tbody>
    </table>
    <input v-model.number="this.nbPoint" type="number" :disabled="this.match.getIsFinished()"/>
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
  float: left;
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
</style>