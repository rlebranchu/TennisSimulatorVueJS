<script lang="ts">

export default {
  props: {
    label: String,
    onClick: Function,
    disabled: Boolean,
  }
}
</script>

<template>
  <button @click="onClick" :disabled="disabled">{{label}}</button>
</template>

<style scoped>
button {
  font-family: 'Montserrat', sans-serif;
  background-color: transparent;
  border: 2px solid black;
  border-radius: 10px;
  color: black;
  padding: 10px;
  font-weight: bold;
}
button:disabled,
button[disabled]{
  border: 1px solid #a5a5a5;
  color: #a5a5a5;
}
</style>