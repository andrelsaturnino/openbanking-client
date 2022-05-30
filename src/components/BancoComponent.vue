<template>
  <v-container fluid class="d-flex justify-center">
    <div class=" ">
      <div>
        <v-autocomplete
          v-model="bancosSelecionados"
          :items="listaBancos"
          item-text="nome"
          item-value="codigo"
          dense
          chips
          small-chips
          label="Roberta"
          multiple
          solo
          clearable
        ></v-autocomplete>
      </div>

      <v-container class="d-flex justify-space-around" fluid>
        <v-checkbox
          v-for="item in keyClientes"
          :key="item"
          v-model="selected"
          :label="item"
          :value="item"
        ></v-checkbox>
      </v-container>
    </div>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    value: null,
    bancosSelecionados: [],
    listaBancos: [],
    clientes: [],
    dadosClientes: [],
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
