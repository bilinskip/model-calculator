<template>
    <div>
        <p class="error">{{error}}</p>
    </div>
</template>

<script>
    export default {
        props: {
            error: String
        }
        
    }
</script>

<style scoped>
.error {
    margin-top: 5px;
    margin-bottom: 25px;
    color: red;
    font-size: 14px;
    font-style: italic;
    text-align: left;
    margin-left: 20%;
}

</style>