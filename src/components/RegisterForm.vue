<template>
    <body>
        <div id="container">
            <Transition name="slide-fade">
                <div v-if="showL" id="login-box">
                    <div class="first-box">
                        <div class="title">
                            <h1>Junte-se a nossa legião de apostadores.</h1>
                        </div>
                        <div id="login-button">
                            <button @click="showRegister">Cadastrar-se</button>
                        </div>

                    </div>
                    <div class="second-box">
                        <div class="title">
                            <h1>Login</h1>
                        </div>
                        <form action="" class="form-info">

                            <div class="input-container">
                                <input id="login-mail" type="email" placeholder="E-mail de acesso" v-model="loginMail">
                            </div>
                            <div class="input-container">
                                <input id="login-password" type="password" placeholder="Senha de acesso"
                                    v-model="loginPassword">
                            </div>
                            <div class="input-submit">
                                <input class="submit-button" type="submit" value="Entrar">
                            </div>
                        </form>
                    </div>
                </div>
            </Transition>
            <Transition name="slide-fade">
                <div v-if="showR" id="register-box">
                    <div class="first-box">
                        <div class="title">
                            <h1>Bem vindo de Volta!</h1>
                        </div>
                        <div id="description">
                            <p>Para entrar em sua conta, forneça suas informações de cadastro clicando no botão abaixo.</p>
                        </div>
                        <div id="login-button">
                            <button @click="showLogin">Entrar</button>
                        </div>
                    </div>
                    <div class="second-box">
                        <div class="title">
                            <h1>Crie a sua conta</h1>
                            
                        </div>
                        <Message :msg="msgSuccessRegister" v-if="msgSuccessRegister" />
                        <form action="" class="form-info">
                            <div class="input-container">
                                <input id="usernameregister" type="text" placeholder="Nome completo"
                                    v-model="registerFullName">
                            </div>
                            <div class="input-container">
                                <input id="usermailregister" type="email" placeholder="E-mail para contato"
                                    v-model="registerMail">
                            </div>
                            <div class="input-container">
                                <input id="userphoneregister" type="text" placeholder="Telefone para contato"
                                    v-model="registerPhone">
                            </div>
                            <div class="input-container">
                                <input id="userdocumentregister" type="text" placeholder="Digite seu CPF"
                                    v-model="registerDocument">
                            </div>
                            <div class="input-container">
                                <input id="userpasswordregister" type="password" placeholder="Senha de acesso"
                                    v-model="registerPassword">
                            </div>
                            <div class="input-container">
                                <input id="userpasswordconfirm" type="password" placeholder="Confirme sua senha"
                                    v-model="registerConfirmPassword">
                            </div>
                            <Message id="msg" :msg="msgError" v-show="msgError" />
                            <div class="checkbox-container">
                                <input id="checkbox" type="checkbox" v-model="registerTerms"> <span>Li e concordo com os <a
                                        href="#">termos de
                                        uso</a></span>
                            </div>
                            <div class="input-submit">
                                <input class="submit-button" @click="registerUser" type="submit" value="Finalizar">
                            </div>
                        </form>
                    </div>
                </div>
            </Transition>


        </div>
    </body>
</template>

<script>
import Message from './Message.vue';

export default {
    name: 'RegisterForm',
    data() {
        return {
            showL: Boolean,
            showR: Boolean,
            //login fields
            loginMail: null,
            loginPassword: null,
            //register fields
            registerFullName: null,
            registerMail: null,
            registerPhone: null,
            registerDocument: null,
            registerPassword: null,
            registerConfirmPassword: null,
            registerTerms: null,
            //message fields
            msgError: null,
            msgSuccessRegister: null

        }
    },
    methods: {
        showRegister() {
            this.showL = false;
            this.showR = true;
        },
        showLogin() {
            this.showR = false;
            this.showL = true;
        },
        //registerMethods
        async registerUser(e) {
            e.preventDefault();
            if (this.registerPassword != this.registerConfirmPassword) {
                this.msgError = "As senhas digitadas não conferem!"
                setTimeout(() => {
                    this.msgError = "";
                }, 2500);

            } else {
                const registerInfo = {
                    id: null,
                    name: this.registerFullName,
                    document: this.registerDocument,
                    email: this.registerMail,
                    password: this.registerPassword,
                    phone: this.registerPhone,
                    userType: 3
                }
                //create json with fields
                const registerInfoJson = JSON.stringify(registerInfo);
                //creating the request with the post method

                const request = await fetch("http://localhost:8081/User", {
                    method: "POST",
                    headers: {
                        "Acept": "application/json",
                        "Content-Type": "application/json"
                    },
                    body: registerInfoJson
                })
                    .catch(function (res) {
                        alert("Ops... " +
                            "\n" +
                            "Nossos serviços estão em manutenção, tente novamente mais tarde.")
                    });

                this.msgSuccessRegister = "Cadastro realizado com sucesso!"
                setTimeout(() => {
                    this.msgSuccessRegister = "";
                }, 2500);

            this.registerFullName = "",
            this.registerMail =  "",
            this.registerPhone =  "",
            this.registerDocument =  "",
            this.registerPassword =  "",
            this.registerConfirmPassword =  ""

            }
        }
    },
    components: {
        Message
    }

}




</script>

<style scoped>
* {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#container {
    display: flex;
    overflow: hidden;
    width: 1008px;
    height: 620px;
}

body {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

#login-box {
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
    transition: .5s;
}

#register-box {
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
    transition: .5s;


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
    box-shadow: inset 1px 1px 50px #013141;



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
    font-size: 16px;
    font-weight: bolder;
    color: #013141;
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

/*componente Message*/


/*transição dos formularios*/
.slide-fade-enter-active {
    transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1)
}

.slide-fade-leave-active {
    transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
    transform: translateX(600px);
    opacity: 0;

}
</style>    