<script setup>
import { ref , provide} from "vue";
import inputsComponent from "./components/inputsComponent.vue";
let year = ref("") ;
let month = ref("") ;
let day = ref("") ;
const dataObject = ref({})
const handleUpdateValues = (values) => {
  year.value = values.year; // year.value is now a number
  month.value = values.month; // month.value is now a number
  day.value = values.day; // day.value is now a number
  dataObject.value = {
    "yearNum":year.value,
    "monthNum":month.value,
    "dayNum":day.value
  }
};
provide("finalNums" , dataObject )
</script>

<template lang="pug">
  inputsComponent(@update-values="handleUpdateValues")
</template>

<style scoped lang="scss"></style>
