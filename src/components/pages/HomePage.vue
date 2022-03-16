<script lang="ts">
import AppButton from "../components/AppButton.vue";
import MatchBox from "../components/MatchBox.vue";
import Match from "@/viewmodels/Match";
import { Options, Vue } from "vue-class-component";

@Options({
  props: {},
  components: {
    AppButton,
    MatchBox
  },
  methods: {
    newMatch() {
      this.matchList.push({id: this.matchList.length, match: new Match()});
    },
  },
  data() {
    return {
      matchList: [{id: 0, match: new Match()}],
    };
  },
})
export default class HomePage extends Vue {}
</script>

<template>
  <div>
    <h1>Simulateur de Match de Tennis</h1>
    <AppButton label="Nouveau Match" :onClick="newMatch" />
  </div>
  <template v-for="item in this.matchList" v-bind:key="item.id">
      <MatchBox :match="item.match"/>
  </template>
</template>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
