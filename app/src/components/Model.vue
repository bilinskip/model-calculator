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
        FEFCO202: 'fefco202',
        FEFCO203: 'fefco203',
        FEFCO204: 'fefco204',
        FEFCO205: 'fefco205'
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
          Y: '',
          RL: ''
        },
        W: {
          X: '',
          Y: '',
          RL: '',
        },
        H: {
          X: '',
          Y: '',
          RL: ''
        },
        T: {
          X: '',
          Y: '',

          RL: '',

        },
        CON: {
          X: '',
          Y: '',
          RL: ''
        }
        
      };
      if (this.model.designType == this.FEFCO200){
        /*parametry do liczenia arkusza po X*/
        currentModel.L.X = 2;
        currentModel.W.X = 2;
        currentModel.H.X = 0;
        currentModel.T.X = 4;
        currentModel.CON.X = 30;
        /*Parametry do liczenia arkusza po Y*/
        currentModel.L.Y = 0;
        currentModel.W.Y = 0.5;
        currentModel.H.Y = 1;
        currentModel.T.Y = 1.5;
        currentModel.CON.Y = 0;
        /*Parametry do liczenia długości noża*/
        currentModel.L.RL = 6;
        currentModel.W.RL = 10;
        currentModel.H.RL = 6;
        currentModel.T.RL = 22;
        currentModel.CON.RL = 60;

      }
      else if (this.model.designType == this.FEFCO201){
        /*parametry do liczenia arkusza po X*/
        currentModel.L.X = 2;
        currentModel.W.X = 2;
        currentModel.H.X = 0;
        currentModel.T.X = 4;
        currentModel.CON.X = 30;
        /*Parametry do liczenia arkusza po Y*/
        currentModel.L.Y = 0;
        currentModel.W.Y = 1;
        currentModel.H.Y = 1;
        currentModel.T.Y = 3;
        currentModel.CON.Y = 0;
        /*Parametry do liczenia długości noża*/
        currentModel.L.RL = 8;
        currentModel.W.RL = 16;
        currentModel.H.RL = 6;
        currentModel.T.RL = 30;
        currentModel.CON.RL = 60;
      }
      else if (this.model.designType == this.FEFCO202){
        /*parametry do liczenia arkusza po X*/
        currentModel.L.X = 2;
        currentModel.W.X = 2;
        currentModel.H.X = 0;
        currentModel.T.X = 4;
        currentModel.CON.X = 30;
        /*Parametry do liczenia arkusza po Y*/
        currentModel.L.Y = 0;
        currentModel.W.Y = 1;
        currentModel.H.Y = 1;
        currentModel.T.Y = 3;
        currentModel.CON.Y = 100;
        /*Parametry do liczenia długości noża*/
        currentModel.L.RL = 8;
        currentModel.W.RL = 16;
        currentModel.H.RL = 6;
        currentModel.T.RL = 30;
        currentModel.CON.RL = 860;
      }
      else if (this.model.designType == this.FEFCO203){
        /*parametry do liczenia arkusza po X*/
        currentModel.L.X = 2;
        currentModel.W.X = 2;
        currentModel.H.X = 0;
        currentModel.T.X = 4;
        currentModel.CON.X = 30;
        /*Parametry do liczenia arkusza po Y*/
        currentModel.L.Y = 0;
        currentModel.W.Y = 2;
        currentModel.H.Y = 1;
        currentModel.T.Y = 3;
        currentModel.CON.Y = 0;
        /*Parametry do liczenia długości noża*/
        currentModel.L.RL = 8;
        currentModel.W.RL = 24;
        currentModel.H.RL = 6;
        currentModel.T.RL = 30;
        currentModel.CON.RL = 60;
      }
      else if (this.model.designType == this.FEFCO204){
        /*parametry do liczenia arkusza po X*/
        currentModel.L.X = 2;
        currentModel.W.X = 2;
        currentModel.H.X = 0;
        currentModel.T.X = 4;
        currentModel.CON.X = 30;
        /*Parametry do liczenia arkusza po Y*/
        currentModel.L.Y = 1;
        currentModel.W.Y = 0;
        currentModel.H.Y = 1;
        currentModel.T.Y = 3;
        currentModel.CON.Y = 0;
        /*Parametry do liczenia długości noża*/
        currentModel.L.RL = 12;
        currentModel.W.RL = 12;
        currentModel.H.RL = 6;
        currentModel.T.RL = 36;
        currentModel.CON.RL = 60;
      }
      else if (this.model.designType == this.FEFCO205){
        /*parametry do liczenia arkusza po X*/
        currentModel.L.X = 2;
        currentModel.W.X = 2;
        currentModel.H.X = 0;
        currentModel.T.X = 4;
        currentModel.CON.X = 30;
        /*Parametry do liczenia arkusza po Y*/
        currentModel.L.Y = 1;
        currentModel.W.Y = 0;
        currentModel.H.Y = 1;
        currentModel.T.Y = 3;
        currentModel.CON.Y = 0;
        /*Parametry do liczenia długości noża*/
        currentModel.L.RL = 16;
        currentModel.W.RL = 8;
        currentModel.H.RL = 6;
        currentModel.T.RL = 36;
        currentModel.CON.RL = 60;
      }
      console.log('## current model ', currentModel);

      this.createModel(currentModel);

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