<template>
  <v-container>
    <v-div>
      <v-card
        v-if="produto == dados.produtos.nome"
        class="mx-auto"
        max-width="344"
        outlined
      >
        <v-list-item three-line>
          <v-list-item-content>
            <div class="text-overline mb-4">{{ dados.produtos.nome[0] }}</div>
            <v-list-item-title class="text-h5 mb-1">
              {{ dados.produtos.valor }}
            </v-list-item-title>
            <v-list-item-subtitle
              >Taxa: {{ dados.produtos.taxa }}</v-list-item-subtitle
            >
          </v-list-item-content>
        </v-list-item>
      </v-card>
      <p v-else>Você não possui contratos ativos para este produto</p>
    </v-div>
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
    dados: [],
  }),
  props: { produto: String },
  methods: {
    getProdutos() {
      fetch("http://localhost:3000/relacionamento/id/1")
        .then((response) => response.json())
        .then(
          (res) =>
            (this.dados = {
              ...res,
              produtos: JSON.parse(res.produtos),
              propostas: JSON.parse(res.propostas),
            })
        )
        .catch((err) => console.log(err));
    },
    updateProdutos() {
      console.log(this.produto);
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.produto),
      };

      fetch("http://localhost:3000/relacionamento", requestOptions)
        .then((response) => response.json())
        .then((res) => {
          console.log(res);
        })

        .catch((err) => console.log(err));
    },
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
    this.getProdutos();
  },
};
</script>

<style></style>
