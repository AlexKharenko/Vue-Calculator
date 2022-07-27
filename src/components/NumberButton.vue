<template>
  <button class="btn btn-number" @click="btnFunction(btnValue)">
    {{ btnValue }}
  </button>
</template>

<script>
export default {
  name: "NumberButton",
  props: ["btnValue", "btnFunction"],
};
</script>

<style scoped>
.btn-number {
  background-color: rgb(214, 214, 245);
  border: 2px solid #b4beee;
}
.btn-number:hover {
  background-color: rgb(201, 201, 245);
}
</style>
