<template>
    <div>
    </div>
</template>

<script>
  export default {
    props:{ 
      fefcoType: String
    },
    data(){
      return {
        FEFCO200: 'fefco200',
        FEFCO201: 'fefco201',
        FEFCO202: 'fefco202',
        FEFCO203: 'fefco203',
        FEFCO204: 'fefco204',
        FEFCO205: 'fefco205'
      }
  },
    watch: {
      fefcoType: function(){
        this.setFefcoParameters();
        }
    },
    methods: {
      setFefcoParameters(){
         let currentModel = {
        L: {
          X: '',
          Y: '',
          RL: ''
        },
        W: {
          X: '',
          Y: '',
          RL: ''
        },
        H: {
          X: '',
          Y: '',
          RL: ''
        },
        T: {
          X: '',
          Y: '',
          RL: ''
        },
        CON: {
          X: '',
          Y: '',
          RL: ''
        }
      };
      console.log('## current fefco in fefco comp ', this.fefcoType);
       if (this.fefcoType == this.FEFCO200){
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
      else if (this.fefcoType == this.FEFCO201){
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
      else if (this.fefcoType == this.FEFCO202){
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
      else if (this.fefcoType == this.FEFCO203){
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
      else if (this.fefcoType == this.FEFCO204){
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
      else if (this.fefcoType == this.FEFCO205){
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
      this.$emit('create-fefco-parameters', currentModel);
    }
  }
}
</script>

<style scoped>

</style>