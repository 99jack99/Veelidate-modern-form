<script setup lang="ts"></script>

<template>
  <form action="">
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
</template>

<style scoped>
.input-box {
  display: flex;
  flex-direction: column;
  position: relative;
  margin-block: 30px;
  /* background-color: lightcoral; */
}

.button {
  width: 350px;
  /* padding: 8px 0; */
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
  /*   padding: 8px 0; */
  border: none;
  /* border-bottom: 2px solid #141e46; */
  background-color: #141e46;
  transition: 0.5s;
  border-radius: 10px;
  padding: 10px 20px;
  color: #fff5e0;
}

.input-box input:focus {
  outline: none;
  /* border-color: lightseagreen; */
  /*  box-shadow: 0 1px 0 0 lightseagreen; */
  /* border: 2px solid #141e46; */
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
  /*  background-color: #fff5e0; */
}

input:focus + label,
input:not(:placeholder-shown) + label {
  transform: translateY(-30px);
  color: #141e46;
}
</style>
