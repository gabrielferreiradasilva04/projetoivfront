<template>
    <div class="message-container">
        <p><strong>{{ msg }}</strong></p>
    </div>
</template>

<script>
export default {
    name: 'Message',
    props: {
        msg: String,
    }
};

</script>

<style scoped>
.message-container {
    color: #013141;
    background-color:#e0b64c ;
    border: 2px solid #086788;
    border-radius: 20px;
    width: auto;
    height: auto;
    text-align: center;
    justify-content: center;
    display: flex;  
    padding: 5px 5px 2px 2px
}

</style>