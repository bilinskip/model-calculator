<template>
  <div class="model-div">
    <div v-show="model.designType">
      <Fefco-parameters :fefcoType ="model.designType" @create-fefco-parameters="createFefcoParameters"/>
    </div>
    <p>Area is {{sheetArea}}</p>
    <p>Rule Length is {{ruleLength}}</p>
    <p>{{sheetSize}}</p>
  </div>
</template>

<script>
import FefcoParameters from './FefcoParameters.vue'
export default {
  name: 'Model',
  components: {
    FefcoParameters
  },
  props: {
    model: {
      long: Number,
      width: Number,
      height: Number,
      cardboardType: Number,
      designType: String
    }
  },
  data(){
      return {
        ruleLength: '',
        blankSizeInX: '',
        blankSizeInY: '',
        sheetSize: '',
        sheetArea: '',
      }
  },
  methods: {
    createFefcoParameters(fefcoParameters){
      this.createModel(fefcoParameters);

    },
    createModel(model){
      this.blankSizeInX = this.setBlankSizeInX(model.L.X * this.model.long, model.W.X * this.model.width, model.H.X * this.model.height, model.T.X * this.model.cardboardType, model.CON.X);
      this.blankSizeInY = this.setBlankSizeInY(model.L.Y * this.model.long, model.W.Y * this.model.width, model.H.Y * this.model.height, model.T.Y * this.model.cardboardType, model.CON.Y);
      this.sheetSize = this.setSheetSize(this.blankSizeInX, this.blankSizeInY);      
      this.sheetArea = this.setSheetArea(this.blankSizeInX, this.blankSizeInY);
      this.ruleLength = this.setRuleLength(model.L.RL * this.model.long, model.W.RL * this.model.width, model.H.RL * this.model.height, model.T.RL *  this.model.cardboardType, model.CON.RL);
    },
    
    setSheetSize(blankSizeInX, blankSizeInY){
      return `Sheet Size is ${blankSizeInX}x${blankSizeInY}`;
    },

    setSheetArea(blankSizeInX, blankSizeInY){
      return parseFloat((blankSizeInX * blankSizeInY) / 1000000).toFixed(2);
    },

    setBlankSizeInX(long, width, height, cardboardType, constantValue){
      return long + width + height + cardboardType + constantValue;
    },

    setBlankSizeInY(long, width, height, cardboardType, constantValue){
      return long + width + height + cardboardType + constantValue;
    },

    setRuleLength(long, width, height, cardboardType, constantValue){
      return (long + width + height + cardboardType + constantValue) / 1000;

    }
  }
}
</script>
<style scoped>
  .model-div{
    border: 2px solid black;
    margin-top: 20px;
  }
  
</style>