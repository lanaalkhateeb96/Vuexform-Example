<template>
<!-- eslint-disable-->
  <title>Your new name</title>
  <h1>Vuex Form - Example</h1>
  <Form>
  <p>
    <label>Alphabetic</label>
    <Field name="alphabetic" type="alphabetic" :rules="validatealphabetic"
    placeholder="alphabetic"  class="input"/>
    <ErrorMessage name="alphabetic" class="error" />
  </p>
  <p>
    <label>Alphanumeric</label>
    <Field name="alphanumeric" type="alphanumeric" :rules="validatealphanumeric"
    placeholder="alpha" class="input"/>
    <ErrorMessage name="alphanumeric" class="error"/>

  </p>

  <p>
    <label>Alphanumeric Dash</label>
    <Field name="alphadash" type="alphadash" :rules="validatealphadash"
    placeholder="alphadash" class="input"/>
    <ErrorMessage name="alphadash" class="error"/>

  </p>
  <p>
    <label>Alphanumeric Space</label>
    <Field name="alphaspace" type="alphaspace" :rules="validatealphaspace"
    placeholder="alphaspace" class="input"/>
    <ErrorMessage name="alphaspace" class="error"/>
  </p>
  <p>
    <label>Between</label>
    <Field name="between" type="between" :rules="validatebetween" placeholder="between"
    class="input"/>
    <ErrorMessage name="between" class="error"/>
  </p>
  <p>
    <label>Decimal</label>
    <Field name="decimal" type="email" :rules="validatedecimal"
    placeholder="decimal" class="input"/>
    <ErrorMessage name="decimal" class="error"/>
  </p>
    <p>
    <label>Email</label>
      <Field name="email" type="email" :rules="validateEmail" placeholder="email"
      class="input"/>
      <ErrorMessage name="email" class="error"/>
    </p>
    <p>
      <label>Includes</label>
      <Field name="includes" type="includes" :rules="validateincludes" placeholder="includes"
      class="input"/>
      <ErrorMessage name="includes" class="error"/>
    </p>
    <p>
      <label>Numeric</label>
      <Field name="numeric" type="numeric" :rules="validatenumeric" placeholder="numeric"
      class="input"/>
      <ErrorMessage name="numeric" class="error"/>
    </p>
  <p>
    <label>Required</label>
    <Field name="required" type="required" :rules="validaterequired" placeholder="required"
    class="input"/>
    <ErrorMessage name="required" class="error"/>
  </p>
</Form>
<button>Submit</button>
<h1>Data</h1>
<div>{{this.$store.state.data}}</div>
<h1>Errors</h1>
<div>{{errors}}</div>
</template>
<script>
/* eslint-disable */
import { Form, Field,ErrorMessage} from 'vee-validate';
export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data(){
    return {
      errors:{alphapetic: {error:null},alphanumeric:{error:null},alphanumericdash:{error:null},alphanumericspace:{error:null},
      email:{error:null},includes:{error:null},numeric:{error:null},required:{error:null},between:{error:null},decimal:{error:null}},
    }
  },
  methods:{
    validatealphabetic(value){
      this.$store.state.data.alphabetic=value
      const regex = /^[A-Za-z]+$/;
      if (!regex.test(value)) {
        this.errors.alphapetic.error='Must be a alphabetic value'
        this.errors.alphapetic.touched=true;
        return 'Must be a alphabetic value';
      }
      else {
        this.errors.alphapetic.error=null;
      }
      return true;
    },
    validatealphanumeric(value){
      this.$store.state.data.alpha=value
      const regex = /^[a-z0-9]+([-_\s]{1}[a-z0-9]+)*$/i;
      if (!regex.test(value)) {
        this.errors.alphanumeric.error='Must only contain letters and numbers';
        this.errors.alphanumeric.touched=true;
        return 'Must only contain letters and numbers';
      }
      else {
        this.errors.alphanumeric.error=null;
      }
      return true;
    },
    validatealphadash(value){
      this.$store.state.data.alphaDash=value
      const regex = /^[a-zA-Z0-9-_]+$/;
      if (!regex.test(value)) {
        this.errors.alphanumericdash.error='Must only contain letters and numbers';
        this.errors.alphanumericdash.touched=true;
        return 'Must only contain letters and numbers';
      }
      else {
        this.errors.alphanumericdash.error=null;
      }
      return true;
    },
    validatealphaspace(value){
      this.$store.state.data.alphaSpace=value
      const regex = /^[a-z\d\-_\s]+$/i;
      if (!regex.test(value)) {
        this.errors.alphanumericspace.error='Must only contain letters, numbers or spaces';
        this.errors.alphanumericspace.touched=true;
        return 'Must only contain letters, numbers or spaces';
      }
      else {
        this.errors.alphanumericspace.error=null;
      }
      return true;
    },
    validatebetween(value){
      this.$store.state.data.between=value
      if (!(0<value && value<11||value=='')) {
        this.errors.between.error='Must only contain letters, numbers or spaces';
        this.errors.between.touched=true;
        return 'Must be between 1 and 10';
      }
      else {
        this.errors.between.error=null;
      }
      return true;
    },
    validatedecimal(value){
      this.$store.state.data.decimal=value
      const regex = /^\d*(\.)?(\d{0,2})?$/;
      if (!regex.test(value)) {
        this.errors.decimal.error='Must be a decimal with 2 points';
        this.errors.decimal.touched=true;
        return 'Must be a decimal with 2 points';
      }
      else {
        this.errors.decimal.error=null;
      }
      return true;
    },
    validateEmail(value) {
      this.$store.state.data.email=value
      const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
      if (!regex.test(value)) {
        this.errors.email.error= 'Not a valid email';
        this.errors.email.touched=true;
        return 'Not a valid email';
      }
      else {
        this.errors.email.error=null;
      }
      return true;
    },
    validateincludes(value){
      this.$store.state.data.includes=value
      if (!(value=='foo'|| value=='bar'||value=='')) {
        this.errors.includes.error='is not one of the following: foo, bar';
        this.errors.includes.touched=true;
        return 'is not one of the following: foo, bar';
      }
      else {
        this.errors.includes.error=null;
      }
      return true;

    },
    validatenumeric(value){
      this.$store.state.data.numeric=value
      const regex = /^[0-9a-zA-Z]+$/;
      if (!regex.test(value)) {
        this.errors.numeric.error="Must be a numeric value"
        this.errors.numeric.touched=true;
        return 'Must be a numeric value';
      }
      else {
        this.errors.numeric.error=null;
      }
      return true;
    },
    validaterequired(value){
      this.$store.state.data.required=value
      const regex = /^[\s\t\r\n]*\S+/ig;
      if (!regex.test(value)) {
        this.errors.required.error='Required';
        this.errors.required.touched=true;
        return 'Required';
      }
      else {
        this.errors.required.error=null;
      }
      return true;
    },
  }
};
/* eslint-enable */
</script>

<style>
.input{
  position: absolute;
  left: 270px;
}
.error {
  position: absolute;
  left: 470px;
  color: brown;
  font-weight: bold;
}

</style>
