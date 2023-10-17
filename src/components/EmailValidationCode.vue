<template>
    <dialog id="dialog">
        <div class="container">
            <div class="title-box">
                <h1>Código de Verificação</h1>
            </div>
            <div class="input-veriffication-email-code">
                <input type="text" id="input-code" class="input">
            </div>
            <div class="input">
                <input type="sumbmit" value="Validar">
            </div>
            <div class="information">
                <p>Caso não tenha recebido o código confira o endereço de e-mail fornecido</p>
            </div>
            <div>
                <button @click="close" id="button-close">Voltar</button>
            </div>

        </div>
    </dialog>
</template>

<script>
export default {

    name: 'EmailValidationCode',
    data() {
        code: String;
    },
    props: {
        mailTo: String
    },
    methods:{
        async close(){

           
        }
    }


}
</script>

<style scoped>
* {
    text-align: justify;
    font-family: Arial, Helvetica, sans-serif
}
</style>