<template>
  <div class="back">
    <v-sheet width="420" class="elevation-24 mx-auto spacing-playground pa-5 text-center rounded-xl">
      <div class="title">
        <h1>Registre-se!</h1>
        <br>
      </div>
      <v-form ref="form" v-model="valid" lazy-validation class="rounded-xl spacing-playground pa-10">
        <v-text-field v-model="name" :rules="nameRules" label="Nome Completo" required></v-text-field>

        <v-text-field v-model="userDocument" label="CPF" :rules="userDocumentRules" required
          v-mask="['###.###.###-##']"></v-text-field>

        <v-text-field v-model="phone" :rules="phoneRules" label="Telefone para contato" required
          v-mask="['(##) #####-####']"></v-text-field>

        <v-text-field v-model="email" label="E-mail para contato" :rules="emailRules" required></v-text-field>

        <v-text-field :rules="[passwordRules.required, passwordRules.min]" v-model="password"
          :type="'' ? 'text' : 'password'" name="input-10-1" label="Confirme a senha"></v-text-field>

        <v-text-field :rules="[passwordRules.required, passwordRules.min]" v-model="confirmPassword"
          :type="'' ? 'text' : 'password'" name="input-10-1" label="Confirme a senha"></v-text-field>

        <v-btn :disabled="!valid" color="blue" class="rounded-pill">
          Registrar-se
        </v-btn>
        <br>
        <br>
        <a id="login-router">Já possuo uma Conta</a>
      </v-form>
    </v-sheet>
  </div>
</template>

<script>
import { mask } from "vue-the-mask";


export default {


  name: "RegisterForm",

  data: () => ({
    //registerFields
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'Campo vazio',
    ],
    email: '',
    emailRules: [
      v => !!v || 'Campo vazio',
      v => /.+@.+/.test(v) || 'O e-mail deve ser válido'
    ],
    userDocument: '',
    userDocumentRules: [
      v => !!v || 'Campo vazio',
    ],
    phone: '',
    phoneRules: [
      v => !!v || 'Campo vazio',
    ],
    checkbox: false,
    //password attributes
    password: '',
    confirmPassword: '',
    passwordRules: {
      required: value => !!value || 'Required.',
      min: v => v.length >= 5 || 'Mínimo de 5 caractéres',
    },

  }),

  methods: {
    /**
     * Método que efetua a validação dos campos antes de realizar o registro
     */
    validate() {
      if (this.$refs.form.validate()) {
        this.snackbar = true
      }
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    }
    /**
     * Fim dos métodos que realizam a validação do registro
     */
  },

  directives: {
    mask
  },



}
</script>

<style scoped>
.title {
  color: #F9A825;
  transition: 1s;
}




.back {
  padding: 50px;
  width: 100%;
  height: 100vh;
  background-image: url("../assets/chevrolet-7637024_1280.jpg");
  background-size: cover;
}

#login-router {
  transition: .5s;
}

#login-router:hover {
  color: #F9A825;
  cursor: pointer;
}
</style>


