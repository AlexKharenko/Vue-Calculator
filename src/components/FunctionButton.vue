<template>
  <button
    class="btn btn-function"
    :class="span2 ? 'span-2' : ''"
    @click="btnFunction(btnValue)"
  >
    {{ btnValue }}
  </button>
</template>

<script>
export default {
  name: "FunctionButton",
  props: ["btnValue", "span2", "btnFunction"],
};
</script>

<style scoped>
.btn-function {
  background-color: rgb(104, 104, 255);
  border: 2px solid #b4beee;
}
.btn-function:hover {
  background-color: rgb(132, 132, 251);
}
.span-2 {
  grid-column: span 2;
}
</style>
