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
      <select id="cardboard" v-model="carboardType" @change="setCardboardType">
        <option v-for="type in cardboardTypes" v-bind:value="type.value" v-bind:key="type.text">
          {{ type.text }}
        </option>
      </select>
    </div>
    <div class="form-control">
      <label>Design types</label>
      <select id="design" v-model="designType" 
      @change="setDesignType">
        <option v-for="type in designTypes" v-bind:value="type.value" v-bind:key="type.text">
          {{ type.text }}
        </option>
      </select>
    </div>
      <input type="submit" value="Submit" class="submit-class"/>
    </form>
    <div v-show="errors.length">
      <Errors/>
    </div>
  </div>
</template>

<script>
import Errors from './Errors'
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
      carboardType: '',
      cardboardTypes: [
      { text: 'B', value: '3' },
      { text: 'C', value: '4' },
      { text: 'E', value: '2' }
    ],
      designType: '',
      designTypes: [
      { text: 'fefco 200', value: 'fefco200' },
      { text: 'fefco 201', value: 'fefco201' },
      { text: 'fefco 202', value: 'fefco202' }
    ]
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()
      const modelDimensions = {
        long: Number(this.long),
        width:  Number(this.width),
        height:  Number(this.height),
        cardboardType:  Number(this.cardboardType),
        designType: this.designType
      };
      console.log('## long digits ', modelDimensions.long.toString().length);
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
    },
    setCardboardType(event){
      this.cardboardType = event.target.value;
    },
    setDesignType(event){
      this.designType = event.target.value;
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

</style>
