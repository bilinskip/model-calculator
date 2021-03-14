<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <Inputs @add-model="addModel" />
    <div v-show="model.long">
      <Model :model="model" :parameters="parameters"/>
    </div>
  </div>
</template>

<script>
import json from "../assets/parameters.json";
import Inputs from './Inputs'
import Model from './Model'
export default {
  name: 'Main',
  components :{
    Inputs,
    Model
  },
  props: {
    msg: String
  },
  data() {
    return {
         result: '',
         model: [],
         sheetLong: '',
         sheetWidth: '',
         parameters: json
    }
  },
  methods: {
    addModel(modelDimensions) {
      this.model = modelDimensions;
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #white;
}
h1 {
  color: white;
  font-size: 48px;
}
</style>
