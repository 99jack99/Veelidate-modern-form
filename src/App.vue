<script setup lang="ts">
import { reactive, computed } from "vue";

/* Import methods and validators that you might want */
import { useVuelidate } from "@vuelidate/core";
import {
  required,
  email,
  minLength,
  sameAs,
  helpers,
} from "@vuelidate/validators";

const pwd_condition = helpers.regex(
  /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[#$@!%&*?])[A-Za-z\d#$@!%&*?]{8,30}$/
);

/* 1.  Create models according to fields that you need */
let user_data = reactive({
  name: "",
  email: "",
  password: {
    password: "",
    repeat: "",
  },
});

/* 2. Replicate the field model with rules that you want to be fulfilled */
let user_validations = computed(() => {
  return {
    name: { required },
    email: { required, email },
    password: {
      password: {
        required,
        minLenght: minLength(6),
        pwd_condition: helpers.withMessage(
          "Min 1 uppercase, Min 1 lowercase, Min 1 special character, Min 1 number, Min 8 characters",
          pwd_condition
        ),
      },
      repeat: { sameAs: sameAs(user_data.password.password) },
    },
  };
});

/* 3. Call validation method from vuelidate, 2 params... model and rules */
const v$ = useVuelidate(user_validations, user_data);

/* This method will be our Api(in this case, its just an example) */
const submit = async () => {
  const result = await v$.value.$validate();
  result ? alert("Data sent correctly!🥳") : alert("Please😿, check data");
};
</script>

<template>
  <div class="wall">
    <h1 class="title">Form with Vuelidate</h1>
    <!-- form -->
    <div class="card">
      <img class="logo" src="./assets/Logo.svg" alt="fake logo" />
      <!-- input -->
      <div class="field-box">
        <div class="input-box">
          <!-- 4. Connect your field with your models created -->
          <input
            v-model="user_data.name"
            type="text"
            id="name"
            placeholder=" "
          />
          <label for="name">Name</label>
        </div>
        <!-- We can call out error so we can represent it in our template -->
        <div class="error" v-for="error in v$.name.$errors" :key="error.$uid">
          {{ error.$message }}
        </div>
      </div>
      <!-- input -->
      <div class="field-box">
        <div class="input-box">
          <input
            v-model="user_data.email"
            type="text"
            id="email"
            placeholder=" "
          />
          <label for="email">Email</label>
        </div>
        <div class="error" v-for="error in v$.email.$errors" :key="error.$uid">
          {{ error.$message }}
        </div>
      </div>

      <!-- input -->
      <div class="field-box">
        <div class="input-box">
          <input
            v-model="user_data.password.password"
            type="password"
            id="password"
            placeholder=" "
          />
          <label for="password">Password</label>
        </div>
        <div
          class="error"
          v-for="error in v$.password.password.$errors"
          :key="error.$uid"
        >
          {{ error.$message }}
        </div>
      </div>

      <!-- input -->
      <div class="field-box">
        <div class="input-box">
          <input
            v-model="user_data.password.repeat"
            type="password"
            id="password_repeat"
            placeholder=" "
          />
          <label for="password_repeat">Confirm Password</label>
        </div>
        <div
          class="error"
          v-for="error in v$.password.repeat.$errors"
          :key="error.$uid"
        >
          {{ error.$message }}
        </div>
      </div>

      <!--  buttons -->
      <div class="input-box">
        <button @click="submit()" class="btn">Submit</button>
      </div>
    </div>
    <h3 class="info">
      2023, Made with 💚 by
      <a class="info_link" href="https://github.com/99jack99/">Jackson</a>
    </h3>
  </div>
</template>

<style scoped>
.wall {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  color: #ffffff;
  height: 100vh;
}

.title {
  font-size: 56px;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #099b6d;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 4px 4px 4px rgba(221, 221, 221, 0.767);
}

.logo {
  margin-block: 20px 40px;
}

.field-box {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: center;
}

.input-box {
  display: flex;
  flex-direction: column;
  position: relative;
  margin-block: 15px;
}

input {
  width: 350px;
  border: none;
  background-color: #ffffff;
  transition: 0.5s;
  border-radius: 10px;
  padding: 10px 15px;
  color: #161618;
  font-size: 16px;
}

label {
  position: absolute;
  height: 100%;
  display: flex;
  align-items: center;
  transition: 0.5s;
  color: #3f3f46;
  margin-left: 10px;
  font-weight: 600;
}

.input-box input:focus {
  outline: none;
  border-radius: 10px;
  padding: 10px 20px;
}

input:focus + label,
input:not(:placeholder-shown) + label {
  transform: translateY(-30px);
  color: #161618;
}

.error {
  background-color: #e3073c;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 5px;
  width: 350px;
  font-weight: 700;
  font-size: 14px;
  font-style: italic;
  color: #161618;
}

.btn {
  width: 350px;
  background-color: #3f3f46;
  border-radius: 10px;
  padding: 10px 20px;
  color: white;
  font-size: 16px;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  cursor: pointer;
}

.btn:hover {
  background-color: #161618;
}

.info {
  font-style: italic;
}

.info_link {
  text-decoration: none;
  color: #099b6d;
}

.info_link:hover {
  border-bottom: 1px solid #099b6d;
}
</style>
