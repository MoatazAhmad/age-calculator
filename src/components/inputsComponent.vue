<script setup>
import { ref, defineEmits } from "vue";
import outputsComponent from "./outputsComponent.vue";

const emit = defineEmits(["update-values"]);

const dayINP = ref(null);
const monthINP = ref(null);
const yearINP = ref(null);
const formRef = ref(null);

const validate = () => {
  const dayEl = dayINP.value;
  const dayLabel = dayEl.previousElementSibling;
  const daySpan = dayEl.nextElementSibling;

  const monthEl = monthINP.value;
  const monthLabel = monthEl.previousElementSibling;
  const monthSpan = monthEl.nextElementSibling;

  const yearEl = yearINP.value;
  const yearLabel = yearEl.previousElementSibling;
  const yearSpan = yearEl.nextElementSibling;

  let isValid = true;

  // Validate day input
  if (dayEl.value === "") {
    dayEl.classList.add("not-valid");
    dayLabel.classList.add("label-n-valid");
    daySpan.classList.remove("d-none");
    daySpan.textContent = "This field is required";
    daySpan.classList.add("n-valid");
    isValid = false;
  } else if (dayEl.value < 1 || dayEl.value > 31) {
    dayEl.classList.add("not-valid");
    dayLabel.classList.add("label-n-valid");
    daySpan.textContent = "Must be a valid day";
    daySpan.classList.remove("d-none");
    daySpan.classList.add("n-valid");
    isValid = false;
  } else {
    dayEl.classList.remove("not-valid");
    dayLabel.classList.remove("label-n-valid");
    daySpan.classList.add("d-none");
    daySpan.classList.remove("n-valid");
  }

  // Validate month input
  if (monthEl.value === "") {
    monthEl.classList.add("not-valid");
    monthLabel.classList.add("label-n-valid");
    monthSpan.classList.remove("d-none");
    monthSpan.textContent = "This field is required";
    monthSpan.classList.add("n-valid");
    isValid = false;
  } else if (monthEl.value < 1 || monthEl.value > 12) {
    monthEl.classList.add("not-valid");
    monthLabel.classList.add("label-n-valid");
    monthSpan.textContent = "Must be a valid month";
    monthSpan.classList.remove("d-none");
    monthSpan.classList.add("n-valid");
    isValid = false;
  } else {
    monthEl.classList.remove("not-valid");
    monthLabel.classList.remove("label-n-valid");
    monthSpan.classList.add("d-none");
    monthSpan.classList.remove("n-valid");
  }

  // Validate year input
  if (yearEl.value === "") {
    yearEl.classList.add("not-valid");
    yearLabel.classList.add("label-n-valid");
    yearSpan.classList.remove("d-none");
    yearSpan.textContent = "This field is required";
    yearSpan.classList.add("n-valid");
    isValid = false;
  } else if (yearEl.value < 1900 || yearEl.value > 2024) {
    yearEl.classList.add("not-valid");
    yearLabel.classList.add("label-n-valid");
    yearSpan.textContent = "Year must be between 1900 and 2024";
    yearSpan.classList.remove("d-none");
    yearSpan.classList.add("n-valid");
    isValid = false;
  } else {
    yearEl.classList.remove("not-valid");
    yearLabel.classList.remove("label-n-valid");
    yearSpan.classList.add("d-none");
    yearSpan.classList.remove("n-valid");
  }

  if (isValid) {
    const yearValue = yearINP.value ? yearINP.value: null;
    const monthValue = monthINP.value ? monthINP.value : null;
    const dayValue = dayINP.value ? dayINP.value : null;
    emit('update-values', { year: yearValue.value, month: monthValue.value, day: dayValue.value })
  }
};
</script>
<template lang="pug">
  div(class="d-flex custom px-5 py-3")
    form(ref="formRef" class="inputs-container d-flex" @submit.prevent="validate")
      div(class="input-part d-flex flex-column")
        label(for="day") DAY
        input(ref="dayINP" type="number" id="day" name="day" placeholder="DD")
        span(class="d-none")
      div(class="input-part d-flex flex-column")
        label(for="month") MONTH
        input(ref="monthINP" type="number" id="month" name="month" placeholder="MM")
        span(class="d-none")
      div(class="input-part d-flex flex-column")
        label(for="year") YEAR
        input(ref="yearINP" type="number" id="year" name="year" placeholder="YYYY")
        span(class="d-none")
      div(class="icon")
        button(class="svg-container" type="submit")
          svg(xmlns="http://www.w3.org/2000/svg" width="46" height="44" viewBox="0 0 46 44")
            g(fill="none" stroke="#FFF" stroke-width="2")
              path(d="M1 22.019C8.333 21.686 23 25.616 23 44M23 44V0M45 22.019C37.667 21.686 23 25.616 23 44")
    outputsComponent
</template>
<style lang="scss">
.custom {
  background: hsl(0, 0%, 100%);
  border-radius: 15px;
  border-bottom-right-radius: 200px;
  width: 700px;
  flex-direction: column;
}
.inputs-container {
  padding: 40px 0;
  border-bottom: 1px solid hsl(0, 0%, 86%);
  position: relative;
}
.input-part {
  max-width: 100%;
  label {
    color: hsl(0, 1%, 44%);
    font-weight: bold;
    font-size: 12px;
    padding-bottom: 5px;
  }

  input {
    font-size: 32px;
    border: 1px solid hsl(0, 0%, 86%);
    border-radius: 10px;
    padding: 10px 16px;
    max-width: 150px;
    cursor: pointer;
    &:focus {
      outline: none;
      border-color: hsl(259, 100%, 65%);
      caret-color: hsl(259, 100%, 65%);
    }
  }
  span {
    max-width: 180px;
    font-size: 14px;
  }
  &:not(:last-of-type) {
    margin-right: 20px;
  }

  .n-valid {
    color: hsl(0, 100%, 67%);
    font-style: italic;
    padding-top: 10px;
  }

  .not-valid {
    border-color: hsl(0, 100%, 67%) !important;
  }

  .label-n-valid {
    color: hsl(0, 100%, 67%);
  }
}

.icon {
  position: absolute;
  right: 0;
  bottom: 0;
  transform: translateY(50%);
}

.svg-container {
  background-color: hsl(259, 100%, 65%);
  padding: 20px;
  text-align: center;
  width: fit-content;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  &:hover {
    background-color: hsl(0, 0%, 8%);
  }
  svg {
    z-index: -1;
  }
}
@media (max-width:520px) {
  .custom {
    width: 380px;
    padding:  0 .5rem !important;
  }
  .inputs-container {
    padding: 40px 0 100px;
    input {
      max-width: 100px ;
    }
  }
  .icon {
    right: 50%;
    bottom: 0;
    transform: translate(50%, 50%);
  }
}
@media (min-width:520px) and (max-width:729px) {
  .custom {
    width: 500px;
  }
  .inputs-container {
    padding: 40px 0 100px;
    input {
      max-width: 125px ;
    }
  }
  .icon {
    right: 50%;
    bottom: 0;
    transform: translate(50%, 50%);
  }
}

</style>