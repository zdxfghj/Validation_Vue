
<template>
  <div class="root">
    <h2>Create an Account</h2>
    <p>
      <input type="text" class="form-control" placeholder="Email" v-model="email" id="email" :class="v$.email.$error? 'is-invalid' : ''"  />
      <span v-if="v$.email.$error" class="invalid-feedback ">
        {{ v$.email.$errors[0].$message }}
      </span>
    </p>
    <p>
      <input type="password" placeholder="Password" v-model="password.password" class="form-control" :class="v$.password.password.$error ? 'is-invalid' : ''" />
      <span v-if="v$.password.password.$error" class="invalid-feedback ">
        {{ v$.password.password.$errors[0].$message }}
      </span>
    </p>
    <p>
      <input type="password" placeholder="Confirm Password" v-model="password.confirm" class="form-control" :class="v$.password.confirm.$error ? 'is-invalid' : ''"/>
      <span v-if="v$.password.confirm.$error" class="invalid-feedback " >
        {{ v$.password.confirm.$errors[0].$message }}
      </span>
    </p>
    <button @click="submitForm">Submit</button>
  </div>
</template>

<script>
import useValidate from '@vuelidate/core';
import { required, minLength,sameAs } from '@vuelidate/validators';

export default {
  data() {
    return {
       v$: useValidate(),
      email: '',
      password: {
        password: '',
        confirm: '',
      }
    }
  },
  methods: {
    submitForm() {
      this.v$.$validate() // checks all inputs
      if (!this.v$.$error) {
        // if ANY fail validation
       console.log("Sucsses")
      } else {
        console.log("Error")
      }
    },
  },
  validations() {
    return {
      email: { required },
      password: {
        password: { required, minLength: minLength(6) },
      confirm: { required, sameAs: sameAs(this.password.password) },
      },
    }
  }
}
</script>


<style lang="css">


.root {
  width: 400px;
  margin: 0 auto;
  color: #2B2D42;
  background-color: #BDE0FE;
  padding: 30px;
  margin-top: 100px;
  border-radius: 20px;
}
input {
  border: none;
  border-radius: 2rem;
  outline: none;
  font-size: 1em;
  padding: 5px 0;
  margin: 10px 0 5px 0;
  width: 100%;
}
button {
  background-color: #457B9D;
  padding: 10px 20px;
  margin-top: 10px;
  border: none;
  border-radius: .7rem;
  color: white;
}


p{
  height: 3rem;
 
}

</style>