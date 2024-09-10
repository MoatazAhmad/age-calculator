<script setup>
import { inject, watchEffect, ref } from "vue";

// Injecting the data
const nums = inject("finalNums", {
  yearNum: null,
  monthNum: null,
  dayNum: null,
});

// Variables to store the final age result
const years = ref(0);
const months = ref(0);
const days = ref(0);

watchEffect(() => {
  if (nums.value.yearNum !== null && nums.value.monthNum !== null && nums.value.dayNum !== null) {
    const today = new Date();
    const birthDate = new Date(nums.value.yearNum, nums.value.monthNum - 1, nums.value.dayNum); // months are zero-based in JS
    
    // Calculate years difference
    years.value = today.getFullYear() - birthDate.getFullYear();

    // Adjust for months and days
    months.value = today.getMonth() - birthDate.getMonth();
    days.value = today.getDate() - birthDate.getDate();

    // If the month difference is negative, subtract a year and adjust months
    if (months.value < 0) {
      years.value--;
      months.value += 12;
    }

    // If the day difference is negative, adjust months and calculate days properly
    if (days.value < 0) {
      months.value--;
      // Calculate the previous month’s number of days
      const lastMonth = new Date(today.getFullYear(), today.getMonth(), 0).getDate();
      days.value += lastMonth;
    }

  }
});
</script>

<template lang="pug">
  div(class="spans-box d-flex flex-column align-items-start py-5")
    div.age-box
      span.num {{ years ? years : "--" }} 
      span.unit years
    div.age-box
      span.num {{ months ? months : "--" }} 
      span.unit months
    div.age-box
      span.num {{ days ? days : "--" }} 
      span.unit days
</template>

<style lang="scss">
.age-box {
  font-size: 70px;
  font-weight: bold;
  .num {
    color: hsl(259, 100%, 65%);
  }
}
</style>
