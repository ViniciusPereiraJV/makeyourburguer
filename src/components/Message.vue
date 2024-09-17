<template>
   <div class="message-container">
    <p>{{msg}}</p>
   </div>
</template>
<script>
export default {
    name:"Message",
    props:{
        "msg": String
    }
}
</script>
<style scoped>
.message-container{
    color: #ffff;
    background-color: #03970b;
    border: 2px solid #03970b;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
}

</style>