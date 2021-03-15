<template>
  <div class="model-div">
    <p>Area is {{sheetArea}}</p>
    <p>Rule Length is {{ruleLength}}</p>
    <p>{{sheetSize}}</p>
  </div>
</template>

<script>

export default {
  name: 'Model',
  props: {
    model: {
      long: Number,
      width: Number,
      height: Number,
      cardboardType: Number,
      designType: String
    },
    parameters: {}
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
  watch:{
    model: function(){
      this.setModel();
    }
  },
  methods: {
    setModel(){
        const model = this.parameters[this.model.designType];
        this.createModel(model);
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
  margin-top: 20px;
  width: 50%;
  margin-left:auto;
  margin-right: auto;
  border: 5px solid white;
  border-radius: 10px;
  color: white;
  font-size: 24px;
  }
  
</style>