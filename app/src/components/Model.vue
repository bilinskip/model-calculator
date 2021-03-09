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
    }
  },
  data(){
      return {
        ruleLength: '',
        blankSizeInX: '',
        blankSizeInY: '',
        sheetSize: '',
        sheetArea: '',
        FEFCO200: 'fefco200',
        FEFCO201: 'fefco201',
        FEFCO202: 'fefco202'
      }
  },
  watch: {
    model: function(){
      this.setModel();
    }
  },
  methods: {
    setModel(){
      let currentModel = {
        L: {
          X: '',
          Y: ''
        },
        W: {
          X: '',
          Y: ''
        },
        widthInX: '',
        widthInY: '',
        height: '',
        constantValueForX: '',
        cardboardTypes: {
          inX: '',
          inY: ''
        },
      };
      if (this.model.designType == this.FEFCO200){
        currentModel.long =  2*this.model.long;
        currentModel.widthInX = 2*this.model.width;

        
      }
      else if (this.model.designType === this.FEFCO201){
        currentModel.long =  2*this.model.long;
        currentModel.widthInX = 2*this.model.width;
        currentModel.widthInY = this.model.width;
        currentModel.height = this.model.height;
        currentModel.constantValueForX = 30;
        currentModel.cardboardTypes.inX = 4*this.model.cardboardType;
        currentModel.cardboardTypes.inY = 3*this.model.cardboardType;
      }
      /*else if (this.model.designType === this.FEFCO202){
        this.createFefco201(this.model);
      }*/
      console.log('## current model ', currentModel);
      this.createModel(currentModel);

    },
    createModel(model){
      this.blankSizeInX = this.setBlankSizeInX(model.long, model.widthInX, model.cardboardTypes.inX, model.constantValueForX);
      this.blankSizeInY = this.setBlankSizeInY(model.height, model.widthInY, model.cardboardTypes.inY);
      this.sheetSize = this.setSheetSize(this.blankSizeInX, this.blankSizeInY);      
      this.sheetArea = this.setSheetArea(this.blankSizeInX, this.blankSizeInY);
     /* this.model.ruleLength = this.setRuleLength(model.valuesForRuleLength.long, model.valuesForRuleLength.width, model.valuesForRuleLength.cardboardType,  model.valuesForRuleLength.height, model.valuesForRuleLength.constantValue);*/

    },
    createFefco200(model){
      console.log('model in fefco 200 ', model);
      this.blankSizeInX = this.setBlankSizeInX(2*model.long, 2*model.width, 4*model.cardboardType, 30);
      console.log('X ', this.blankSizeInX);
      this.blankSizeInY = this.setBlankSizeInY(model.height, model.width/2, 3*model.cardboardType);
      this.sheetSize = this.setSheetSize(this.blankSizeInX, this.blankSizeInY);      
      this.sheetArea = this.setSheetArea(this.blankSizeInX, this.blankSizeInY);
      this.ruleLength = this.setRuleLength(6*model.long, 10*model.width, 22*model.cardboardType,  6*model.height, 60);
    },
     createFefco201(model){
      console.log('model in fefco 201 ', model);
      this.blankSizeInX = this.setBlankSizeInX(2*model.long, 2*model.width, 4*model.cardboardType, 30);
      this.blankSizeInY = this.setBlankSizeInY(model.height, model.width, 3*model.cardboardType);
      this.sheetSize = this.setSheetSize(this.blankSizeInX, this.blankSizeInY);
      this.sheetArea = this.setSheetArea(this.blankSizeInX, this.blankSizeInY);
      this.ruleLength = this.setRuleLength(8*model.long, 16*model.width, 30*model.cardboardType,  6*model.height, 60);
    },
     createFefco202(model){
      console.log('model in fefco 202 ', model);
      this.blankSizeInX = this.setBlankSizeInX(2*model.long, 2*model.width, 4*model.cardboardType, 30);
      this.blankSizeInY = this.setBlankSizeInY( model.height, model.width, 3*model.cardboardType);
      this.sheetSize = this.setSheetSize(this.blankSizeInX, this.blankSizeInY);
      this.sheetArea = this.setSheetArea(this.blankSizeInX, this.blankSizeInY);
     this.ruleLength = this.setRuleLength(8*model.long, 16*model.width, 30*model.cardboardType,  6*model.height, 860);
    },


    setSheetSize(blankSizeInX, blankSizeInY){
      return `Sheet Size is ${blankSizeInX}x${blankSizeInY}`;
    },

    setSheetArea(blankSizeInX, blankSizeInY){
      return parseFloat((blankSizeInX * blankSizeInY) / 1000000).toFixed(2);
    },

    setBlankSizeInX(long, width, cardboardType, constantValue){
      return long + width + cardboardType + constantValue;
    },

    setBlankSizeInY(height, width, cardboardType){
      return height + width + cardboardType;
    },

    setRuleLength(long, width, height, cardboardType, constantValue){
      return (long + width + cardboardType + height + constantValue) / 1000;

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