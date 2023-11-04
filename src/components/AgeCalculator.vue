<template>
  <div class="main">
    <div class="container">
      <form class="date-form">
        <div>
          <label>DAY</label>
          <input
            id="day"
            type="text"
            placeholder="DD"
            v-model="inputDay"
            @input="errorMessages"
          />
          <i class="error" id="day-msg" v-if="errorDayMessage">{{
            errorDayMessage
          }}</i>
        </div>

        <div>
          <label>MONTH</label>
          <input
            id="month"
            type="text"
            placeholder="MM"
            v-model="inputMonth"
            @input="errorMessages"
          />
          <i class="error" id="month-msg" v-if="errorMonthMessage">{{
            errorMonthMessage
          }}</i>
        </div>

        <div>
          <label>YEAR</label>
          <input
            id="year"
            type="text"
            placeholder="YYYY"
            v-model="inputYear"
            @input="errorMessages"
          />
          <i class="error" id="year-msg" v-if="errorYearMessage">{{
            errorYearMessage
          }}</i>
        </div>
      </form>
      <div class="arrowline">
        <button @click="calculateAge">
          <img :src="require('../assets/iconarrow.svg')" alt="ArrowImage" />
        </button>
      </div>
      <div class="content">
        <p>
          <span>{{ birthYear }}</span
          >years
        </p>
        <p>
          <span>{{ birthMonth }}</span
          >months
        </p>
        <p>
          <span>{{ birthDay }}</span
          >days
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const inputDay = ref("");
const inputMonth = ref("");
const inputYear = ref("");
let birthDay = ref("");
let birthYear = ref("");
let birthMonth = ref("");
/* let errorMessageDay = inputDay.value > 31;
let errorMessageMonth = inputMonth.value > 12;
let errorMessageYear = inputYear.value > 2023; */
let errorDayMessage = ref("");
let errorMonthMessage = ref("");
let errorYearMessage = ref("");
const currentDate = new Date();
const errorMessages = () => {
  if (inputDay.value > 31 && inputMonth.value > 12 && inputYear.value > 2023) {
    errorDayMessage = "Must be a valid day";
    errorMonthMessage = "Must be a valid Month";
    errorYearMessage = "Must be in the past";
  } else if (
    inputDay.value === "" &&
    inputMonth.value === "" &&
    inputYear.value === ""
  ) {
    errorDayMessage = "This field is required";
    errorMonthMessage = "This field is required";
    errorYearMessage = "This field is required";
  } else {
    errorDayMessage = "";
    errorMonthMessage = "";
    errorYearMessage = "";
  }
};
const calculateAge = () => {
  const birthDate = new Date(
    inputYear.value,
    inputMonth.value - 1,
    inputDay.value
  );

  if (inputDay.value > 31 && inputMonth.value > 12 && inputYear.value > 2023) {
    birthYear.value = "_ _";
    birthMonth.value = "_ _";
    birthDay.value = "_ _";
    /*  errorDayMessage = "Must be a valid day";
    errorMonthMessage = "Must be a valid Month";
    errorYearMessage = "Must be in the past"; */
  } else if (
    inputDay.value === "" &&
    inputMonth.value === "" &&
    inputYear.value === ""
  ) {
    birthYear.value = "_ _";
    birthMonth.value = "_ _";
    birthDay.value = "_ _";
    errorDayMessage = "This field is required";
    errorMonthMessage = "This field is required";
    errorYearMessage = "This field is required";
  } else {
    // Calculate age and update data properties
    const ageInMilliseconds = currentDate - birthDate;
    const ageDate = new Date(ageInMilliseconds);
    const years = ageDate.getUTCFullYear() - 1970;
    const months = ageDate.getUTCMonth();
    const days = ageDate.getUTCDate() - 1;
    /* errorDayMessage = "";
    errorMonthMessage = "";
    errorYearMessage = ""; */
    birthYear.value = years;
    birthMonth.value = months;
    birthDay.value = days;
  }
};
</script>

<style>
.main {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background-color: hsl(0, 0%, 94%);
}

.container {
  width: 45%;
  border-radius: 20px;
  border-bottom-right-radius: 40%;
  background-color: white;
  position: relative;
  padding: 60px;
}

.date-form {
  display: flex;
  gap: 30px;
  margin-top: 30px;
}

.date-form div {
  display: flex;
  flex-direction: column;
}

.content span {
  color: hsl(259, 100%, 65%);
  margin-right: 10px;
}

label {
  color: hsl(0, 1%, 44%);
  letter-spacing: 0.2rem;
}

input {
  width: 85px;
  border-radius: 3px;
  border: 1px solid hsl(0, 0%, 86%);
  font-size: 22px;
  font-weight: bolder;
  padding: 6px 8px;
}

.arrowline {
  position: relative;
  width: 100%;
  height: 2px;
  background: lightgray;
  margin: 50px auto;
}

.arrowline button {
  position: absolute;
  right: 0;
  top: -30px;
}

hr {
  width: 75%;
  text-align: center;
  border: none;
  border-top: 1px solid lightgray;
  margin-top: 36px;
  margin-right: 1px;
  margin-left: 32px;
}

button {
  width: 65px;
  height: 65px;
  border-radius: 50%;
  border: none;
  margin-left: 0;
  background-color: hsl(259, 100%, 65%);
  cursor: pointer;
}

button:hover {
  background-color: black;
  color: white;
}

button img {
  width: 30px;
  height: 50px;
  padding: 5px;
}

.content {
  font-style: italic;
  font-weight: bold;

  /* background-color: blue; */
}

.content p::before {
  /* content: "---"; */
  color: hsl(259, 100%, 65%);
  font-size: 30px;
  margin-right: 10px;
}
.content p {
  font-size: 50px;
  margin: 0;
  padding: 0;
}

.error {
  color: hsl(0, 100%, 67%);
  font-size: 12px;
}
</style>
