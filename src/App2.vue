<script setup lang="ts">
import { useVuelidate } from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";
import { reactive } from "vue";

let user_data = reactive({
  user: "",
  email: "",
});

let user_validations = {
  user: { required },
  email: { required, email },
};

const v$ = useVuelidate(user_validations, user_data);

const submit = () => {
  const result = v$.value.$validate();

  console.log(result);
};
</script>

<template>
  <!-- form -->
  <div class="card">
    <!-- input -->
    <div class="boxy">
      <div class="input-box">
        <input
          v-model="user_data.user"
          type="text"
          id="email"
          placeholder=" "
        />
        <label for="email">User</label>
      </div>
      <div class="errorbox" v-for="error in v$.user.$errors" :key="error.$uid">
        {{ error.$message }}
      </div>
    </div>
    <!-- input -->
    <div class="boxy">
      <div class="input-box">
        <input
          v-model="user_data.email"
          type="text"
          id="email"
          placeholder=" "
        />
        <label for="email">Email</label>
      </div>
      <div class="errorbox" v-for="error in v$.email.$errors" :key="error.$uid">
        {{ error.$message }}
      </div>
    </div>

    <!--  buttons -->
    <div class="input-box">
      <button @click="submit()" class="button">Submit</button>
    </div>
  </div>
</template>

<style scoped>
.boxy {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: center;
}
.errorbox {
  background-color: red;
  padding: 10px 10px;
  border-radius: 10px;
  margin-block: 5px 10px;
  width: 350px;
}
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
  margin-block: 10px;
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
  border: none;
}

/* .testi {
  width: 350px;
  border: none;
  background-color: #141e46;
  transition: 0.5s;
  border-radius: 10px;
  padding: 10px 20px;
  color: #fff5e0;
} */

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
