<template>
  <div class="main">
    <div class="container">
      <form class="date-form">
        <div>
          <label :class="dayErr.showErr ? 'error' : ''">DAY</label>
          <input
            type="text"
            required
            maxlength="2"
            placeholder="DD"
            v-model="inputDay"
            @input="errorMessages"
            :class="dayErr.showErr ? 'inputError' : ''"
          />
          <i class="error" id="day-msg" v-if="dayErr.showErr">{{
            dayErr.message
          }}</i>
        </div>

        <div>
          <label :class="monthErr.showErr ? 'error' : ''">MONTH</label>
          <input
            type="text"
            required
            maxlength="2"
            placeholder="MM"
            v-model="inputMonth"
            @input="errorMessages"
            :class="monthErr.showErr ? 'inputError' : ''"
          />
          <i class="error" v-if="monthErr.showErr">{{ monthErr.message }}</i>
        </div>

        <div>
          <label :class="yearErr.showErr ? 'error' : ''">YEAR</label>
          <input
            type="text"
            required
            maxlength="4"
            placeholder="YYYY"
            v-model="inputYear"
            @input="errorMessages"
            :class="monthErr.showErr ? 'inputError' : ''"
          />
          <i class="error" id="year-msg" v-if="yearErr.showErr">{{
            yearErr.message
          }}</i>
        </div>
      </form>
      <div class="arrowline">
        <button @click="calculateAge">
          <img src="../assets/iconarrow.svg" alt="ArrowImage" />
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
import { ref, reactive } from "vue";
let inputDay = ref("");
let inputMonth = ref("");
let inputYear = ref("");
let birthDay = ref("");
let birthYear = ref("");
let birthMonth = ref("");

const currentDate = new Date();

const dayErr = reactive({ message: "", showErr: false });
const monthErr = reactive({ message: "", showErr: false });
const yearErr = reactive({ message: "", showErr: false });

const errorMessages = () => {
  if (inputDay.value > 31) {
    dayErr.showErr = true;
    dayErr.message = "Must be a valid day";
  } else {
    dayErr.showErr = false;
  }

  if (inputMonth.value > 12) {
    monthErr.message = "Must be a valid Month";
    monthErr.showErr = true;
  } else {
    monthErr.showErr = false;
  }

  if (inputYear.value > 2023) {
    yearErr.showErr = true;
    yearErr.message = "Must be in the past";
  } else {
    yearErr.showErr = false;
  }

  if (
    inputDay.value >= 31 &&
    (parseInt(inputMonth.value) === 4 ||
      parseInt(inputMonth.value) === 6 ||
      parseInt(inputMonth.value) === 9 ||
      parseInt(inputMonth.value) === 11)
  ) {
    dayErr.showErr = true;
    dayErr.message = "Must be a valid date";
  }
};
const calculateAge = () => {
  const birthDate = new Date(
    inputYear.value,
    inputMonth.value - 1,
    inputDay.value
  );

  if (inputDay.value === "") {
    dayErr.message = "Enter value for day";
    dayErr.showErr = true;
  } else {
    dayErr.showErr = false;
  }
  if (inputMonth.value === "") {
    monthErr.message = "Enter value for month";
    monthErr.showErr = true;
  } else {
    dayErr.showErr = false;
  }
  if (inputYear.value === "") {
    yearErr.message = "Enter value for year";
    yearErr.showErr = true;
  } else {
    yearErr.showErr = false;
  }

  if (
    inputDay.value === inputDay.value &&
    inputMonth.value === "" &&
    inputYear.value === inputYear.value
  ) {
    monthErr.message = "Enter value for month";
    monthErr.showErr = true;
    birthDate.value = "_ _";
    birthMonth.value = "_ _";
    birthYear.value = "_ _";
  } else {
    monthErr.showErr = false;
  }

  if (inputDay.value > 31 && inputMonth.value > 12 && inputYear.value > 2023) {
    birthYear.value = "_ _";
    birthMonth.value = "_ _";
    birthDay.value = "_ _";
  } else if (
    parseInt(inputDay.value) >= 31 &&
    (parseInt(inputMonth.value) === 4 ||
      parseInt(inputMonth.value) === 6 ||
      parseInt(inputMonth.value) === 9 ||
      parseInt(inputMonth.value) === 11) &&
    inputYear.value >= 1970
  ) {
    birthYear.value = "_ _";
    birthMonth.value = "_ _";
    birthDay.value = "_ _";
  } else if (
    inputDay.value === "" &&
    inputMonth.value === "" &&
    inputYear.value === ""
  ) {
    birthYear.value = "_ _";
    birthMonth.value = "_ _";
    birthDay.value = "_ _";
  } else {
    // Calculate age and update data properties
    const ageInMilliseconds = currentDate - birthDate;
    const ageDate = new Date(ageInMilliseconds);
    const years = ageDate.getUTCFullYear() - 1970;
    const months = ageDate.getUTCMonth();
    const days = ageDate.getUTCDate() - 1;
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
  width: 40%;
  height: 70%;
  border-radius: 20px;
  border-bottom-right-radius: 40%;
  background-color: white;
  /* position: relative; */
  padding: 10px 60px;
  margin-top: 0;
}

.date-form {
  display: flex;
  gap: 30px;
  margin-top: 20px;
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
  letter-spacing: 0.1rem;
  font-weight: 0;
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
  margin-top: 40px;
  margin-bottom: 30px;
}

.arrowline button {
  position: absolute;
  right: 0;
  top: -30px;
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
  font-size: 14px;
}

@media screen and (max-width: 600px) {
  .container {
    width: 90%;
    padding: 10px;
    position: relative;
  }

  input {
    width: 60px;
  }

  .arrowline button {
    position: absolute;
    /* top: 40%; */
    left: 40%;
  }

  .date-form {
    gap: 20px;
    margin: 0;
  }
}

.inputError {
  border: 1px solid red;
}
</style>
