<template>
  <div class="gender_wpapper">
    <form @submit="getGender">
      <input
        placeholder="Enter your name..."
        type="text"
        v-model="genderName"
      />
      <button>Find out gender</button>
    </form>
    <span class="answer">{{ answer }} </span>
  </div>
</template>

<script>
import { serverUrl, defaultValueAnswer, defaultValue } from "./const";

export default {
  data() {
    return {
      genderName: defaultValue,
      answer: defaultValueAnswer,
    };
  },
  methods: {
    async getGender(event) {
      event.preventDefault();
      if (this.genderName !== defaultValue) {
        const url = `${serverUrl}?name=${this.genderName}`;
        const response = await fetch(url);
        const result = await response.json();
        this.answer = await result.gender;
        this.genderName = defaultValue;
      } else {
        this.answer = defaultValueAnswer;
      }
    },
  },
};
</script>

<style>
* {
  margin: 0 auto;
  padding: 0;
  box-sizing: border-box;
}

.gender_wpapper {
  width: 240px;
  height: 80px;
  background-color: rgb(66, 65, 65);
  text-align: center;
  margin-top: 300px;
  border-radius: 5px;
}

.gender_wpapper input {
  margin-top: 10px;
  border: none;
  border-radius: 5px;
  width: 150px;
  height: 20px;
}

.gender_wpapper button {
  margin-top: 5px;
}

.answer {
  color: white;
  font-size: 15px;
}
</style>
