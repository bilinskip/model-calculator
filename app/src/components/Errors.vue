<template>
    <div class="errors-class">
        <b>Please correct the following error(s):</b>
        <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
    </div>
</template>

<script>
  export default {
    props:{
      errors: []
    }
  }
</script>

<style scoped>
.errors-class{
  margin-top: 10px;
  color: red;
}
li {
  list-style-type: none;
  padding: 2px;
}

</style>