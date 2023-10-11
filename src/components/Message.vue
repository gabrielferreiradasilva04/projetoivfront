<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name: 'Message',
    props: {
        msg: String
    }
};

</script>

<style scoped>
.message-container {
    color: #013141;
    background-color:#B8DAFF ;
    border: 2px solid #086788;
    border-radius: 20px;
    width: 300px;
    height: 40px;
    text-align: center;
    justify-content: center;
    display: flex;  
}

</style>