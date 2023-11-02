<template>
  <div class="main">
    <div class="container">
      <div class="form">
        <form action="#">
          <label>DAY</label>
          <input type="text" placeholder="DD" />
          <label>MONTH</label>
          <input type="text" placeholder="MM" />
          <label>YEAR</label>
          <input type="text" placeholder="YYYY" />
        </form>
        <div class="arrowline">
          <hr />
          <button @click="AgeCalculatorapp">
            <img :src="arrImage" alt="ArrowImage" />
          </button>
        </div>
      </div>

      <div class="content">
        <p class="year"><span>--</span>years</p>
        <p class="month"><span>--</span>months</p>
        <p class="days"><span>--</span>days</p>
      </div>
    </div>
  </div>
</template>

<script>
import ArrowImage from "../assets/iconarrow.svg";
export default {
  data() {
    return {
      arrImage: ArrowImage,
    };
  },

  /* method: {
    AgeCalculatorApp() {
      let CurrentDate = new Date();
    },
  }, */
};
</script>

<style>
.main {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 1440px;
  height: 100vh;
  background-color: hsl(0, 0%, 94%);
}

.container {
  width: 700px;
  height: 550px;
  border-radius: 16px;
  border-bottom-right-radius: 40%;
  background-color: white;
  position: relative;
  padding: 10px;
  /* justify-content: center; */
}

form {
  display: flex;
  text-align: center;
  /* margin: 30px 30px 0 0; */
  margin-top: 30px;
}

label {
  font-family: "Poppins", sans-serif;
  color: hsl(0, 1%, 44%);
}

input {
  width: 75px;
  height: 40px;
  color: hsl(0, 0%, 86%);
  margin-top: 30px;
  border-radius: 3px;
  border: 1px solid hsl(0, 0%, 86%);
  padding-left: 10px;
  font-family: "Poppins", sans-serif;
  font-style: none;
  font-size: 20px;
}

.arrowline {
  display: flex;
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

button:focus {
}

button img {
  width: 30px;
  height: 50px;
  padding: 8px;
}

.content {
  font-family: "Poppins", sans-serif;
  font-style: italic;
  font-weight: bold;
  font-size: 85px;
  margin: 30px;
  position: absolute;
  top: 18%;
}

.container p {
  margin-bottom: 50px;
}

span {
  color: hsl(259, 100%, 65%);
  margin-right: 10px;
}

.year {
  position: absolute;
  bottom: 10px;
}
.month {
  margin-top: 30px;
  position: relative;
  top: 70px;
}
.days {
  /* background: red; */
  width: 100%;
  margin-bottom: 60px;
  position: absolute;
  top: 50%;
}

@media screen and (max-width: 1440px) {
  .form {
    zoom: normal;
  }
}
</style>
