<template>
  <v-container>
    <v-form>
      <v-container>
        <v-alert
          v-if="feedback"
          border="top"
          :color="error ? 'red' : 'green'"
          dark
          >{{ error ? messages.error : messages.sucess }}</v-alert
        >
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="clientes[0].nome"
              label="Nome"
              outlined
              disabled
            ></v-text-field>

            <v-text-field
              v-model="clientes[0].datanascimento"
              label="Data de Nascimento"
              outlined
              disabled
            ></v-text-field>
            <v-text-field
              v-model="clientes[0].telefone"
              label="Telefone"
              outlined
            ></v-text-field>
          </v-col>

          <v-col cols="12" sm="6">
            <v-text-field
              v-model="clientes[0].cpf"
              label="CPF"
              outlined
              disabled
            ></v-text-field>
            <v-text-field
              v-model="clientes[0].endereco"
              label="Endereço"
              outlined
            ></v-text-field>
            <v-text-field
              v-model="clientes[0].email"
              label="E-mail"
              outlined
            ></v-text-field>
          </v-col>
        </v-row>
        <v-btn rounded color="primary" dark @click="updateDados">
          Salvar
        </v-btn>
      </v-container>
    </v-form>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    value: null,
    bancosSelecionados: [],
    listaBancos: [],
    clientes: [],
    keyClientes: [],
    selected: [],
    messages: { sucess: "Salvo com sucesso", error: "Não foi possível salvar" },
    feedback: false,
  }),

  methods: {
    getBancos() {
      fetch("http://localhost:3000/bancos")
        .then((response) => response.json())
        .then((res) => (this.listaBancos = res))
        .catch((err) => console.log(err));
    },
    getClientes() {
      fetch("http://localhost:3000/clientes")
        .then((response) => response.json())
        .then((res) => {
          this.clientes = res;
          this.getArrayofCliente(this.clientes);
        })

        .catch((err) => console.log(err));
    },
    getArrayofCliente(obj) {
      this.keyClientes = Object.keys(obj[0]);
    },
    updateDados() {
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.clientes[0]),
      };

      fetch("http://localhost:3000/clientes", requestOptions)
        .then((res) => {
          this.feedback = true;
          res.status != 201 ? (this.error = true) : (this.error = false);
        })
        .catch((err) => {
          console.log("err");
          console.log(err);
        });
    },
  },

  created() {
    this.getBancos();
    this.getClientes();
  },
};
</script>

<style></style>
