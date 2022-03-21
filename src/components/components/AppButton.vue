<script lang="ts">

export default {
  props: {
    label: String,
    onClick: Function,
    disabled: Boolean,
    size: {
      default: "B",
      type: String
    }
  }
}
</script>

<template>
  <button v-on:click="onClick" :disabled="disabled" v-bind:class="{'bigButton': size=='B'}">{{label}}</button>
</template>

<style scoped>
button {
  font-family: 'Montserrat', sans-serif;
  background-color: transparent;
  border: 2px solid black;
  border-radius: 10px;
  color: black;
  font-weight: bold;
}
button:disabled,
button[disabled]{
  border: 1px solid #a5a5a5;
  color: #a5a5a5;
}
.bigButton {
  padding: 10px;
}
</style>