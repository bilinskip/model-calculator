<template>
<div class="input-div">
    <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Long</label>
      <input type="number" v-model="long" name="long" class="input-element">
       <div v-if="errors[0]">
        <InlineError :error="errors[0]"/>
      </div>
    </div>
    <div class="form-control">
      <label>Width</label>
      <input type="number" v-model="width" name="width" class="input-element">
       <div v-if="errors[1]">
        <InlineError :error="errors[1]"/>
      </div>
    </div>
    <div class="form-control">
      <label> Height</label>
      <input type="number" v-model="height" name="height" class="input-element">
      <div v-if="errors[2]">
        <InlineError :error="errors[2]"/>
      </div>
    </div>
    <div class="form-control">
      <label>Cardboard types</label>
        <v-select label="text" :options="cardboardTypeOptions" v-model="cardboardType"></v-select>
         <div v-if="errors[3]">
        <InlineError :error="errors[3]"/>
      </div>
    </div>
     <div class="form-control">
      <label>Design types</label>
     <v-select label="text" :options="designTypeOptions" v-model="designType"></v-select>
      <div v-if="errors[4]">
        <InlineError :error="errors[4]"/>
      </div>
    </div>
    
      <input type="submit" value="Submit" class="submit-class"/>
    </form>
    <!-- <div v-if="errors.length" class="errors-class">
      <Errors :errors="errors"/>
    </div> -->
  </div>
</template>

<script>
// import Errors from './Errors.vue'
import InlineError from './InlineError.vue'
import newFefcoJSON from "../assets/newFefco.json"
import cardboardTypesJSON from "../assets/cardboardTypes.json"
import Vue from 'vue'
import vSelect from 'vue-select'

import 'vue-select/dist/vue-select.css';

Vue.component('v-select', vSelect)
export default {
  name: 'Inputs',
  components: {
    // Errors,
    InlineError
  },
  data() {
    return {
      errors: [],
      long: '',
      width: '',
      height: '',
      cardboardType: '',
      cardboardTypeOptions: cardboardTypesJSON,
      designType: '',
      designTypeOptions: newFefcoJSON
    }
  },
  methods: {
    setDesignTypes(){
    },
    onSubmit(e) {
      e.preventDefault()
      const modelDimensions = {
        long: Number(this.long),
        width:  Number(this.width),
        height:  Number(this.height),
        cardboardType:  this.cardboardType.value,
        designType: this.designType.value
      };
      console.log('## model dims ', modelDimensions);
       this.errors = [];
      if (!modelDimensions.long){
        this.errors.push("*Long is required");
      }
      if (!modelDimensions.width){
        this.errors.push("*Width is required");
      }
      if (!modelDimensions.height){
        this.errors.push("*Height is required");
      }
      if (!modelDimensions.cardboardType){
        this.errors.push("*Cardboard Type is required");
      }
      if (!modelDimensions.designType){
        this.errors.push("*Design Type is required");
      }
      if (modelDimensions.width > modelDimensions.long){
        this.errors.push("model Long has to be greater than model Width");
      }
      if (modelDimensions.long.toString().length > 4
        || modelDimensions.width.toString().length > 4
        || modelDimensions.height.toString().length > 4){
          this.errors.push("Each model dimension has to be lower than 10000");
        }

        console.log("errors ", this.errors);
        console.log("errors [long] ", this.errors[0]);
      
      if (!this.errors.length) {
        this.$emit('add-model', modelDimensions);
      }
      else {
        this.$emit('add-model', []);
      }

      
     /* this.long = '';
      this.width = '';
      this.height = '';
      this.cardboardType = '';
      this.designType = '';*/
    }
  }
}
</script>

<style scoped>
.input-div{
  width: 50%;
  margin-left:auto;
  margin-right: auto;
  border: 5px solid white;
  border-radius: 10px;
}
.form-control{
  margin: 10px 0;
}
.form-control label {
  display: block;
  color: white;
  font-size: 17px;
}
/* .form-control input {
  width: 80%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
} */
.submit-class {
  margin-top: 25px;
  margin-bottom: 25px;
  width: 25%;
  height: 40px;
  font-size: 20px;
  font-weight: 700;
  color: white;
  border: 1px solid grey;
  border-radius: 10px;
  background-color: #009EDB;
  transition: 500ms;
  opacity: 0.6;
}
.submit-class:hover {
   opacity: 1;
}
.submit-class:focus {
  outline: none;
}
.v-select {
  width: 60%;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
    border: 1px solid grey; 
    -webkit-box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    -moz-box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    background: white;
     border-radius: 10px;

} 

.input-element {
  width: 56%;
  font-size: 17px;
  color: black;
    border: 1px solid grey; 
    -webkit-box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    -moz-box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    padding: 15px;
    background: white;
    margin: 0 0 10px 0;
    border-radius: 10px;
}
</style>
