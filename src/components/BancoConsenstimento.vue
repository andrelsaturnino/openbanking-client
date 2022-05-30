<template>
  <v-container fluid class="d-flex justify-center">
    <div class="">
      <div>
        <v-autocomplete
          v-model="consentimento.bancos"
          :items="listaBancos"
          item-text="nome"
          item-value="codigo"
          dense
          deletable-chips
          chips
          small-chips
          label="Selecione o(s) Banco(s)"
          multiple
          solo
          clearable
        ></v-autocomplete>
      </div>

      <v-container class="d-flex justify-space-around" fluid>
        <v-checkbox
          class="mr-4"
          v-for="item in dadosClientes"
          :key="item"
          v-model="consentimento.dados_consentidos"
          :label="item"
          :value="item"
        ></v-checkbox>
      </v-container>

      <v-btn rounded color="primary" dark @click="postConsentimento">
        Salvar
      </v-btn>
    </div>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    value: null,
    consentimento: { bancos: [], cliente: 1, dados_consentidos: [] },
    listaBancos: [],
    clientes: [],
    dadosClientes: [
      "Nome",
      "CPF",
      "Data de Nascimento",
      "Telefone",
      "Email",
      "Endereço",
    ],
    keyClientes: [],
    selected: [],
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
    postConsentimento() {
      console.log(this.consentimento);
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.consentimento),
      };

      fetch("http://localhost:3000/relacionamento", requestOptions)
        .then((response) => response.json())
        .then((res) => {
          console.log(res);
        })

        .catch((err) => console.log(err));
    },

    getArrayofCliente(obj) {
      this.keyClientes = Object.keys(obj[0]);
    },
  },
  created() {
    this.getBancos();
    this.getClientes();
  },
};
</script>

<style></style>
