<template>
  <div class="d-flex justify-center">
    <v-card>
      <v-tabs v-model="tab" background-color="primary" dark>
        <v-tab v-for="item in items" :key="item.tab">
          <v-icon>{{ item.icon }}</v-icon>
          {{ item.tab }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tab">
        <v-tab-item>
          <div class="my-4 text-subtitle-1">
            <v-card flat class="d-flex justify-space-around">
              <MeusDados />
            </v-card>
          </div>
        </v-tab-item>
        <v-tab-item>
          <div class="my-4 text-subtitle-1">
            <v-card flat class="d-flex justify-space-around">
              <v-col>
                <p>Produtos</p>
                <ProdutosCliente produto="Crédito Comercial" />
              </v-col>
              <v-col>
                <p>Propostas</p>
                <PropostasCliente produto="Crédito Comercial" />
              </v-col>
            </v-card>
          </div>
        </v-tab-item>
        <v-tab-item>
          <div class="my-4 text-subtitle-1">
            <v-card flat class="d-flex justify-space-around">
              <v-col>
                <p>Produtos</p>
                <ProdutosCliente produto="Crédito Consignado" />
              </v-col>
              <v-col>
                <p>Propostas</p>
                <PropostasCliente produto="Crédito Consignado" />
              </v-col>
            </v-card>
          </div>
        </v-tab-item>
        <v-tab-item>
          <div class="my-4 text-subtitle-1">
            <v-card flat class="d-flex justify-space-around">
              <v-col>
                <p>Produtos</p>
                <ProdutosCliente produto="Cartão de Crédito" />
              </v-col>
              <v-col>
                <p>Propostas</p>
                <PropostasCliente produto="Cartão de Crédito" />
              </v-col>
            </v-card>
          </div>
        </v-tab-item>
        <v-tab-item>
          <div class="my-4 text-subtitle-1">
            <v-card flat class="d-flex justify-space-around">
              <v-col>
                <p>Produtos</p>
                <ProdutosCliente produto="Seguro de Vida" />
              </v-col>
              <v-col>
                <p>Propostas</p>
                <PropostasCliente produto="Seguro de Vida" />
              </v-col>
            </v-card>
          </div>
        </v-tab-item>
        <v-tab-item>
          <div class="my-4 text-subtitle-1">
            <v-card flat class="d-flex justify-space-around">
              <BancoConsenstimento />
            </v-card>
          </div>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </div>
</template>

<script>
import BancoConsenstimento from "./BancoConsenstimento.vue";
import MeusDados from "./MeusDados.vue";
import ProdutosCliente from "./ProdutosCliente.vue";
import PropostasCliente from "./PropostasCliente.vue";

export default {
  data() {
    return {
      tab: null,

      items: [
        {
          icon: "mdi-account",
          tab: "Meus Dados",
          content: "Andre Luiz",
          propostas: "tetetetetete",
        },
        { tab: "Crédito Comercial", content: "Tab 2 Content", propostas: "2" },
        { tab: "Consignado", content: "Tab 3 Content", propostas: "3" },
        { tab: "Cartão de Crédito", content: "Tab 4 Content", propostas: "4" },
        { tab: "Seguridade", content: "Tab 5 Content", propostas: "5" },
        { tab: "Consentimento", content: "<BancoComponent />" },
      ],
    };
  },

  components: {
    BancoConsenstimento,
    MeusDados,
    ProdutosCliente,
    PropostasCliente,
  },
};
</script>

<style>
.tabs {
  justify-content: space-around;
  width: 100%;
  font-size: 11px;
  height: 220px;
}
</style>
