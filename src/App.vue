<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";
let data = ref();

const llamada = () => {
  axios
    .get("http://www.boredapi.com/api/activity/")
    .then((res) => console.log(res.data))
    .catch((res) => console.log(res));
};

llamada();
</script>

<template>
  <form action="" class="card">
    <div class="input-box">
      <input type="text" id="name" placeholder=" " />
      <label for="name">Name</label>
    </div>
    <div class="input-box">
      <input type="text" id="email" placeholder=" " />
      <label for="email">Email</label>
    </div>
    <div class="input-box">
      <input type="password" id="pwd" placeholder=" " />
      <label for="pwd">Password</label>
    </div>

    <div class="input-box">
      <div class="button">Submit</div>
    </div>
  </form>

  <div></div>
</template>

<style scoped>
.card {
  background-color: lightblue;
  padding: 10px 30px;
  border-radius: 20px;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}
.input-box {
  display: flex;
  flex-direction: column;
  position: relative;
  margin-block: 30px;
}

.button {
  width: 350px;
  background-color: #f78ca2;
  border-radius: 10px;
  padding: 10px 20px;
  color: #191717;
  display: flex;
  justify-content: center;
  align-items: center;
}

input {
  width: 350px;
  border: none;
  background-color: #141e46;
  transition: 0.5s;
  border-radius: 10px;
  padding: 10px 20px;
  color: #fff5e0;
}

.input-box input:focus {
  outline: none;
  border-radius: 10px;
  padding: 10px 20px;
}

label {
  position: absolute;
  height: 100%;
  display: flex;
  align-items: center;
  transition: 0.5s;
  color: #fff5e0;
  margin-left: 10px;
}

input:focus + label,
input:not(:placeholder-shown) + label {
  transform: translateY(-30px);
  color: #141e46;
}
</style>
