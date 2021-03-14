<template>
<div>
    <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Long</label>
      <input type="number" v-model="long" name="long">
    </div>
    <div class="form-control">
      <label>Width</label>
      <input type="number" v-model="width" name="width">
    </div>
    <div class="form-control">
      <label> Height</label>
      <input type="number" v-model="height" name="height">
    </div>
    <div class="form-control">
      <label>Cardboard types</label>
        <v-select label="text" :options="cardboardTypeOptions" v-model="cardboardType"></v-select>
    </div>
     <div class="form-control">
      <label>Design types</label>
     <v-select label="text" :options="designTypeOptions" v-model="designType"></v-select>
    </div>
    
      <input type="submit" value="Submit" class="submit-class"/>
    </form>
    <div v-if="errors.length" class="errors-class">
      <Errors :errors="errors"/>
    </div>
  </div>
</template>

<script>
import Errors from './Errors.vue'
import newFefcoJSON from "../assets/newFefco.json"
import cardboardTypesJSON from "../assets/cardboardTypes.json"
import Vue from 'vue'
import vSelect from 'vue-select'
import 'vue-select/dist/vue-select.css';

Vue.component('v-select', vSelect)
export default {
  name: 'Inputs',
  components: {
    Errors
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
        this.errors.push("Long is required");
      }
      if (!modelDimensions.width){
        this.errors.push("Width is required");
      }
      if (!modelDimensions.height){
        this.errors.push("Height is required");
      }
      if (!modelDimensions.cardboardType){
        this.errors.push("Cardboard Type is required");
      }
      if (!modelDimensions.designType){
        this.errors.push("Design Type is required");
      }
      if (modelDimensions.width > modelDimensions.long){
        this.errors.push("model Long has to be greater than model Width");
      }
      if (modelDimensions.long.toString().length > 4
        || modelDimensions.width.toString().length > 4
        || modelDimensions.height.toString().length > 4){
          this.errors.push("Each model dimension has to be lower than 10000");
        }
      
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
.form-control{
  margin: 10px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 80%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.submit-class {
  width: 80%;
  height: 60px;
  font-size: 20px;
  font-weight: 700;
}
.v-select {
  width: 50%;
  margin-left: auto;
  margin-right: auto;
}

</style>
