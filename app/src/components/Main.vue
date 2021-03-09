<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <Inputs @add-model="addModel" />
    <div v-show="model.long">
      <Model :model="model"/>
    </div>
  </div>
</template>

<script>
import Inputs from './Inputs'
import Model from './Model'
export default {
  name: 'Main',
  props: {
    msg: String
  },
  data() {
    return {
         result: '',
         model: [],
         sheetLong: '',
         sheetWidth: ''
    }
  },
  methods: {
    addModel(modelDimensions) {
      this.model = modelDimensions;
    }
  },
  components :{
    Inputs,
    Model
  },
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
  color: #42b983;
}
</style>
