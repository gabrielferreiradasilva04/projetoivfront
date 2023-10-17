
<template>
  <div class="register-message-box">
    <Transition name="bounce">
      <Message id="msg" :msg="msg" v-show="msg" />
    </Transition>
  </div>



  <body>

    <dialog id="terms">
      <Terms />
    </dialog>

    <div id="container">
      <Transition name="slide-fade">
        <div v-if="showL" id="login-box">
          <div class="first-box">
            <div class="title">
              <h1>Junte-se a nossa legião de apostadores.</h1>
            </div>
            <div class="button-redirect">
              <button @click="showRegister">Cadastrar-se</button>
            </div>
          </div>
          <div class="second-box">
            <div class="title">
              <h1>Login</h1>
            </div>
            <form action="" class="form-info">
              <div class="input-container">
                <input id="login-mail" type="email" placeholder="E-mail de acesso" v-model="loginMail" />
              </div>
              <div class="input-container">
                <input id="login-password" type="password" placeholder="Senha de acesso" v-model="loginPassword" />
              </div>
              <div class="input-submit">
                <input class="submit-button" type="submit" value="Entrar" />
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
              <p>
                Para entrar em sua conta, forneça suas informações de cadastro
                clicando no botão abaixo.
              </p>
            </div>
            <div class="button-redirect">
              <button @click="showLogin">Entrar</button>
            </div>
          </div>
          <div class="second-box">
            <div class="title">
              <h1>Crie a sua conta</h1>
            </div>
            <form action="" class="form-info">
              <div class="input-container">
                <input id="usernameregister" type="text" placeholder="Nome completo" v-model="registerFullName"
                  required />
              </div>
              <div class="input-container">
                <input id="usermailregister" type="email" placeholder="E-mail para contato" v-model="registerMail"
                  required />
              </div>
              <div class="input-container">
                <input required id="userphoneregister" type="text" placeholder="Telefone para contato" v-mask="['(##) #####-####']"
                  v-model="registerPhone" />
              </div>
              <div class="input-container">
                <input required id="userdocumentregister" type="text" placeholder="Digite seu CPF" v-model="registerDocument"
                  v-mask="['###.###.###-##']" />
              </div>
              <div class="input-container">
                <input required @focusin="showPassword" @focusout="hidePassword" id="userpasswordregister" type="password"
                  placeholder="Senha de acesso" v-model="registerPassword" />
              </div>
              <div class="input-container">
                <input required id="userpasswordconfirm" type="password" placeholder="Confirme sua senha"
                  v-model="registerConfirmPassword" />
              </div>
              <div class="checkbox-container">
                <input required id="checkbox" type="checkbox" v-model="registerTerms" />
                <span><button id="button-terms" @click="showTerms">Eu li e aceito os <a href="#">termos de
                      uso</a></button></span>
              </div>
              <div class="input-submit">
                <input class="submit-button" @click="registerUser" type="submit" value="Próximo" />
              </div>
            </form>
          </div>
        </div>
      </Transition>
      <div v-if="showEmailValidation" id="validation-box">
        <div class="first-box">
          <div class="title">
            <h1>Validação do E-mail.</h1>
          </div>
          <div class="button-redirect">
            <button @click="showRegister">Voltar</button>
          </div>
        </div>
        <div class="second-box">
          <div class="subtitle">
            <p>Caso não tenha recebido o código, volte ao registro e verifique seu e-mail</p>
          </div>
          <form action="" class="form-info">
            <div class="input-container">
              <input required placeholder="Digite o código de verificação" type="text" id="verificationCode" v-model="registerVerificationCode">
            </div>
            <div class="input-submit">
              <input type="submit" value="Finalizar" class="submit-button">
            </div>
          </form>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
import Message from "./Message.vue";
import { mask } from "vue-the-mask";
import Terms from "./Terms.vue"


export default {

  name: "RegisterForm",
  data() {
    return {
      showL: Boolean,
      showR: Boolean,
      showEmailValidation: Boolean,
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
      registerVerificationCode: null,
      //message fields
      msg: null
    };
  },
  /**
   * diretivas utilizadas dentro do documento html, essa diretiva foi importada
   */
  directives: {
    mask
  },
  /**
   * Métodos criados dentro do documento
   */
  methods: {
    /**
     * Métodos para a transição do login e do registro
     */
    showRegister() {
      this.showL = false;
      this.showEmailValidation = false;
      this.showR = true;
    },
    showLogin() {
      this.showR = false;
      this.showEmailValidation = false;
      this.showL = true;
    },
    showEmailValidationView() {
      this.showR = false;
      this.showEmailValidation = true;
      this.showL = false;
    },
    /**
     * Fim dos métodos para transição de login e registro
     */
    /***
     * método para abrir a janela de termos
     */
  async showTerms(e){
      e.preventDefault()
      const dialog = document.querySelector("#terms");
      dialog.showModal();
    },
    /**
     * Método para realizar a inserção de um usuario dentro do sistema
     * 
     * @param {} e 
     */
    async registerUser(e) {
      /***
       * User register with
       */
      e.preventDefault();
      //creating the fields
      const registerInfo = {
        id: null,
        name: this.registerFullName,
        document: this.registerDocument,
        email: this.registerMail,
        password: this.registerPassword,
        confirmPassword: this.registerConfirmPassword,
        phone: this.registerPhone,
        userType: 3,
      };
      //create json with fields
      const registerInfoJson = JSON.stringify(registerInfo);
      //creating the request with the post method
      const request = await fetch("http://localhost:8081/User", {
        method: "POST",
        headers: {
          Acept: "application/json",
          "Content-Type": "application/json",
        },
        body: registerInfoJson,
      }).then((res) => {
        if (res.status === 404) {
          return res.json().then((data) => {
            const error = data;
            this.msg = error;
            setTimeout(() => {
              this.msg = "";

            }, 8000);
          })
        }else{
          if(res.status === 201){
            this.sendEmailValidationCode();
          }
        }
      })
    },
    /**
     * Método para o envio do código de validação do e-mail do usuário * 
     * @param {*} e 
     */
    async sendEmailValidationCode(e) {


      //montando o e-mail

      const emailInfo = {
        mailTo: this.registerMail
      };

      //transformando os dados em um json para enviar no cabeçalho da requisição para a api

      const emailInfoJson = JSON.stringify(emailInfo);

      const request = await fetch("http://localhost:8081/Email", {
        method: "POST",
        headers: {
          Acept: "application/json",
          "Content-Type": "application/json",
        },
        body: emailInfoJson,
      }).then((res) => {
        if (res.status === 404) {

          return res.json().then((data) => {

            const error = data;
            this.msg = error;
            setTimeout(() => {
              this.msg = "";

            }, 8000);

          })

        } else {
          if (res.status === 201) {
            
            this.showEmailValidationView()
            
            //mostrar o aviso do envio do e-mail para validação
            this.msg = "Um código de verificação foi enviado para:" + this.registerMail
            setTimeout(() => {
              this.msg = "";
            }, 5000);




          }
        }
      })

    },
    /**
     * Função para mostrar o dialog dos termos de uso
     * @param {} e 
     */
    /**
     * função para mostrar a senha do usuario
     */
    async showPassword() {
      const password = document.getElementById("userpasswordregister");
      password.setAttribute('type', 'text');

    },
    /**
     * Função para ocultar a senha do usuario
     */
    async hidePassword() {
      const password = document.getElementById("userpasswordregister");
      password.setAttribute('type', 'password');
    }
  },

  components: {
    Message,
    Terms,
  },

};
</script>

<style scoped>
* {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

#container {
  display: flex;
  overflow: hidden;
  width: 1008px;
  height: 620px;
  position: relative;
}

dialog {
  width: 60%;
  height: 60%;
  opacity: 93%;
  border: 4px #013141 solid;
}


body {
  width: 100%;
  height: 90vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
}

#login-box {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  border: 4px solid #f0c808;
  border-radius: 87px;
  height: 500px;
  width: 1000px;
  column-count: 2;
  margin: 0 auto;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  position: relative;
  transition: 0.5s;
}

#register-box {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  border: 4px solid #f0c808;
  border-radius: 87px;
  height: 500px;
  width: 1000px;
  column-count: 2;
  margin: 0 auto;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  position: relative;
  transition: 0.5s;
}
#validation-box {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  border: 4px solid #f0c808;
  border-radius: 87px;
  height: 500px;
  width: 1000px;
  column-count: 2;
  margin: 0 auto;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  position: relative;
  transition: 0.5s;
}
.subtitle{
  padding-top: 0px;

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
  color: #f0c808;
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

.button-redirect {
  padding-top: 30px;
  align-items: center;
  justify-content: center;
}

.button-redirect button {
  font-weight: bold;
  font-size: 16px;
  width: 120px;
  height: 45px;
  background: transparent;
  border: solid 4px #f0c808;
  border-radius: 50px;
  color: #f0c808;
  transition: 0.5s;
}

.button-redirect button:hover {
  cursor: pointer;
  background-color: #ffff;
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
  border: solid 4px #f0c808;
  border-radius: 50px;
  color: #f0c808;
  transition: 0.5s;
}

.input-submit .submit-button:hover {
  background-color: #07a0c3;
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
  color: #f0c808;
}

a {
  color: #f0c808;
}

.title {
  align-items: center;
  display: flex;
  justify-content: center;
}

.register-message-box {
  display: flex;
  justify-content: center;
  align-items: center;
}

#button-terms {
  background-color: transparent;
  font-weight: bold;
  font-size: 16px;
  border: none;
  cursor: pointer;
}

/*componente Message*/

/*transição dos formularios*/
.slide-fade-enter-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(600px);
  opacity: 0;
}

/*Componente message*/
.bounce-enter-active {
  animation: bounce-in 0.5s;
}


@keyframes bounce-in {
  0% {
    transform: scale(0);
  }

  50% {
    transform: scale(1.25);
  }

  100% {
    transform: scale(1);
  }
}
</style>
