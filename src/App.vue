<template>
  <card>
    <div class="main-content">
      <div class="box-imput">
        <div class="single-imput">
          <label>Day</label>
          <input
            type="text"
            placeholder="DD"
            id="Day"
            required
            v-model="dayInput"
          />
          <div class="error">{{ dayError }}</div>
        </div>
        <div class="single-imput">
          <label>Month</label>
          <input
            type="text"
            placeholder="MM"
            id="month"
            required
            v-model="monthInput"
          />
          <div class="error">{{ monthError }}</div>
        </div>
        <div class="single-imput">
          <label>YEAR</label>
          <input
            type="text"
            placeholder="YYYY"
            id="Year"
            required
            v-model="yearInput"
          />
          <div class="error">{{ yearError }}</div>
        </div>
      </div>
      <div class="button-content">
        <div class="line"></div>
        <button id="submit" @click="handleClick">
          <img src="./assets/icon-arrow.svg" />
        </button>
        <button class="reset-btn" @click="resetBtn">
          <img src="./assets/reset.png" />
        </button>
        <div class="lime-sec"></div>
      </div>
      <div class="result-view">
        <span>{{ yearOutput }}</span> years
      </div>
      <div class="result-view">
        <span>{{ monthOutput }}</span> months
      </div>
      <div class="result-view">
        <span>{{ dayOutput }}</span> days
      </div>
    </div>
  </card>
  <!-- <link rel="stylesheet" href="./components/style.css"> -->
  <Calculator />
</template>



<script setup>
import { ref } from "vue";
import Calculator from "./components/Calculator.vue";

const dayInput = ref("");
const monthInput = ref("");
const yearInput = ref("");

const dayOutput = ref("--");
const monthOutput = ref("--");
const yearOutput = ref("--");

const dayError = ref(null);
const monthError = ref(null);
const yearError = ref(null);

const displayError = "incorect";

var monthLength = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
var monthDays = monthLength[Number(monthInput.value)];

const currentYear = new Date().getFullYear().toString();

const letsCheckTheDate = () => {
  const dateStr = Date.parse(
    monthInput.value + "/" + dayInput.value + "/" + yearInput.value
  );
  // subtract user date form todays date
  const dateDiff = new Date() - dateStr;

  let newDiff = Math.floor(dateDiff / (1000 * 60 * 60 * 24));

  if (newDiff < 0) {
    dayError.value = " Day Incorrect";
    monthError.value = "Month incorrect";
    yearError.value = "Your Birth Date cannot be later than today";

    return false;
  } else if (newDiff >= 0) {
    return true;
  } else {
    dayError.value = displayError;
    monthError.value = displayError;
    yearError.value = displayError;
    return false;
  }
};

const handleClick = () => {
  if (
    letsCheckTheDate(Number(dayInput), Number(monthInput), Number(yearInput))
  ) {
    if (letsCheckTheDate()) {
      dayOutput.value = dayInput.value;
      monthOutput.value = monthInput.value;
      yearOutput.value = currentYear - yearInput.value;

      dayError.value = null;
      monthError.value = null;
      yearError.value = null;
    }
  }
};

const resetBtn = () => {
  dayInput.value = "";
  monthInput.value = "";
  yearInput.value = "";

  dayOutput.value = "--";
  monthOutput.value = "--";
  yearOutput.value = "--";

  dayError.value = null;
  monthError.value = null;
  yearError.value = null;
};
</script>














<style>
* {
  box-sizing: border-box;
}

body {
  font-weight: 700;
  font-family: "poppins", sans-serif;
  background: rgb(235, 235, 235);
}

card {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.main-content {
  width: 700px;
  height: 550px;
  background-color: white;
  border-radius: 20px;
  border-bottom-right-radius: 170px;
  padding: 40px;
}

.box-imput {
  display: flex;
  flex-direction: row;
  width: 480px;
  justify-content: space-around;
  color: hsl(0, 1%, 44%);
  text-transform: uppercase;
}

.single-imput {
  display: flex;
  flex-direction: column;
}

.single-imput label {
  letter-spacing: 0.2rem;
  font-size: 12px;
  margin-bottom: 5px;
}

.single-imput input {
  width: 140px;
  padding: 10px;
  padding-left: 20px;
  font-size: 32px;
  font-weight: 700;
  border-radius: 8px;
  border: 1px solid hsl(0, 0%, 86%);
  color: rgb(0, 0, 0);
}

.single-imput input {
  border: 1px solid hsl(259, 100%, 65%);
  outline: none;
}

.error {
  font-size: 12px;
  font-style: italic;
  font-weight: 400;
  color: hsl(0, 100%, 67%);
  text-transform: none;
  margin-top: 10px;
}

.button-content {
  align-items: center;
  flex-direction: row;
  display: flex;
}

.line {
  width: 100%;
  border-bottom: 1px solid hsl(0, 0%, 86%);
}

button {
  padding: 20px;
  border: none;
  border-radius: 50px;
  background-color: rgb(120, 65, 209);
  cursor: pointer;
  transition: 0.8s ease;
}

button:hover {
  background-color: rgb(57, 102, 63);
}

.reset-btn {
  margin-left: 5px;
}

.reset-btn img {
  height: 47px;
  display: flex;
}

reset-img:hover {
  background-color: rgb(141, 44, 20);
}

.result-view {
  font-size: 70px;
  font-weight: 800;
  font-style: italic;
  margin-bottom: -20px;
  color: black;
}

span {
  color: rgb(120, 65, 209);
}

@media (max-width: 600px) {
  .main-content {
    width: auto;
    height: 430px;
    padding: 30px;
    border-bottom-left-radius: 80px;
  }

  .box-imput {
    width: 100%;
  }

  .single-imput input {
    width: 80px;
    font-size: 20px;
    padding: 15px;
  }

  .error {
    width: 90px;
  }

  .button-content {
    margin-top: 20px;
    margin-right: 50px;
  }

  .button img {
    width: 20px;
  }

  .line-sec {
    border: 1px solid hsl(0, 0%, 86%);
    width: 100%;
  }

  .result-view {
    font-size: 50px;
  }
}
</style>
