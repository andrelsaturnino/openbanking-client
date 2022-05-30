<template>
  <v-container>
    <v-div>
      <div
        v-if="
          dados.propostas
            ? dados.propostas.filter((i) => {
                return i.nome == produto;
              })
            : false
        "
      >
        <v-card
          v-for="item in dados.propostas"
          :key="item.nome"
          class="mx-auto mb-5"
          max-width="344"
          outlined
        >
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">{{ item.nome }}</div>
              <v-list-item-title class="text-h5 mb-1">
                {{ item.valor }}
              </v-list-item-title>
              <v-list-item-subtitle>Taxa: {{ item.taxa }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-card-actions>
            <v-btn outlined rounded text @click="contratar(item)">
              Contratar
            </v-btn>
          </v-card-actions>
        </v-card>
      </div>
      <p v-else>Você não possui propostas para este produto</p>
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
        .then((res) => {
          console.log(res);

          this.dados = {
            ...res,
            produtos: JSON.parse(res.produtos),
            propostas: JSON.parse(res.propostas),
          };
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
    contratar(item) {
      //console.log(this.dados.clienteId);

      item.clienteId = this.dados.clienteId;
      //console.log(item);

      const oldProdutos = this.dados.produtos;

      const requestOptions = {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ item, oldProdutos }),
      };

      // console.log(requestOptions);

      fetch("http://localhost:3000/relacionamento/contratar", requestOptions)
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
    this.getProdutos();
  },
};
</script>

<style></style>
