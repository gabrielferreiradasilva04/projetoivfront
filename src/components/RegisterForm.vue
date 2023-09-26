<template>
    <body>
        <div id="container">
            <div id="main-box2">
                <div class="first-box">
                    <div class="title">
                        <h1>Junte-se a nossa legião de apostadores.</h1>
                    </div>
                    <div id="login-button">
                        <button  @click="callRegister">Cadastrar-se</button>
                    </div>

                </div>
                <div class="second-box">
                    <div class="title">
                        <h1>Login</h1>
                    </div>
                    <form action="" class="form-info">

                        <div class="input-container">
                            <input id="usermail" type="email" placeholder="E-mail para contato">
                        </div>
                        <div class="input-container">
                            <input id="userpassword" type="password" placeholder="Senha de acesso">
                        </div>
                        <div class="input-submit">
                            <input class="submit-button" type="submit" value="Entrar">
                        </div>
                    </form>
                </div>
            </div>
            <div id="main-box">
                <div class="first-box">
                    <div class="title">
                        <h1>Bem vindo de Volta!</h1>
                    </div>
                    <div id="description">
                        <p>Para entrar em sua conta, forneça suas informações de cadastro clicando no botão abaixo.</p>
                    </div>
                    <div id="login-button">
                        <button>Entrar</button>
                    </div>

                </div>
                <div class="second-box">
                    <div class="title">
                        <h1>Crie a sua conta</h1>
                    </div>
                    <form action="" class="form-info">
                        <div class="input-container">
                            <input id="usernameregister" type="text" placeholder="Nome completo">
                        </div>
                        <div class="input-container">
                            <input id="usermailregister" type="email" placeholder="E-mail para contato">
                        </div>
                        <div class="input-container">
                            <input id="userphoneregister" type="text" placeholder="Telefone para contato">
                        </div>
                        <div class="input-container">
                            <input id="userdocumentregister" type="text" placeholder="Digite seu CPF">
                        </div>
                        <div class="input-container">
                            <input id="userpasswordregister" type="password" placeholder="Senha de acesso">
                        </div>
                        <div class="input-container">
                            <input id="userpasswordconfirm" type="password" placeholder="Confirme sua senha">
                        </div>
                        <div class="checkbox-container">
                            <input id="checkbox" type="checkbox"> <span>Li e concordo com os <a href="#">termos de
                                    uso</a></span>
                        </div>
                        <div class="input-submit">
                            <input class="submit-button" type="submit" value="Finalizar">
                        </div>
                    </form>
                </div>
            </div>

        </div>
    </body>
</template>
<script>

export default {
    name: 'RegisterForm',
    methods: {
        async callRegister(e) {
            const mainbox2 = document.querySelector('#main-box2');
            const mainbox = document.querySelector('#main-box');
            mainbox2.classList.add('hide-login');
            mainbox.classList.add('show-register');
            
        }
    }
}




</script>

<style scoped>
#container {
    display: flex;
    overflow: hidden;
    width: 1008px;
    height: 609px;
    position: relative;
}

body {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

#main-box {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
    border: 4px solid #F0C808;
    border-radius: 87px;
    height: 600px;
    width: 1000px;
    column-count: 2;
    margin: 0 auto;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: bold;
    position: relative;
}

#main-box2 {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
    border: 4px solid #F0C808;
    border-radius: 87px;
    height: 600px;
    width: 1000px;
    column-count: 2;
    margin: 0 auto;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: bold;
    position: relative;
}

.first-box {
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: #086788;
    height: 100%;
    border-top-left-radius: 87px;
    border-bottom-left-radius: 87px;
    width: 500px;
    color: #F0C808;

}

.title {
    text-align: center;
    align-items: center;
}

#description {
    text-align: center;
    align-items: center;
    font-size: 20px;
    margin: 0 auto;
    padding-left: 15px;
    padding-right: 15px;
}

#login-button {
    padding-top: 30px;
    align-items: center;
    justify-content: center;
}

#login-button button {
    font-weight: bold;
    font-size: 16px;
    width: 120px;
    height: 45px;
    background: transparent;
    border: solid 4px #F0C808;
    border-radius: 50px;
    color: #F0C808;
    transition: .5s;
}

#login-button button:hover {
    cursor: pointer;
    background-color: #FFFF;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
    width: 400px;
}

.input-container input {
    height: 25px;
    border-top: none;
    border-left: none;
    border-right: none;
    border-bottom: solid 2px black;
}

.input-submit {
    display: flex;
    justify-content: center;
    align-items: center;
    padding-top: 30px;
}

.input-submit .submit-button {
    font-weight: bold;
    font-size: 16px;
    width: 120px;
    height: 45px;
    background: transparent;
    border: solid 4px #F0C808;
    border-radius: 50px;
    color: #F0C808;
    transition: .5s;
}

.input-submit .submit-button:hover {
    background-color: #07A0C3;
    cursor: pointer;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
    width: auto;
}

.second-box {
    width: 500px;
    margin: 0 auto;
    padding-left: 20px;
}

.second-box h1 {
    color: #F0C808;
}

a {
    color: #F0C808;
}

.title {
    align-items: center;
    display: flex;
    justify-content: center;
}
.hide-login{
    left: 1010px;
}
.show-register{
    left: -1008px;
    
}

</style>    