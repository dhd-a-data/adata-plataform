<template>
  <div class="q-pa-md q-gutter-md"></div>
  <q-item clickable v-ripple style="margin-top:3em;">
    <q-item-section side>
      <q-avatar>
        <img src="~assets/popcorn-avatr.png">
      </q-avatar>
    </q-item-section>
    <q-item-section @click="nivel = true">
      <q-item-label>Olá, João Pipoqueiro</q-item-label>
      <q-item-label>Nivel 1 - 20/100 XP</q-item-label>
    </q-item-section>
  </q-item>
  <q-list bordered class="rounded-borders" style="max-width: 350px;margin-top: 20px">
    <q-item-label header>Missões</q-item-label>
    <q-separator spaced />
    <q-item clickable v-ripple @click="card = true">
      <q-item-section>
        <q-item-label lines="1">Realize 5 vendas</q-item-label>
        <q-item-label caption lines="2">
        </q-item-label>
      </q-item-section>
      <q-item-section side top>
        <q-icon name="done"></q-icon>
      </q-item-section>
    </q-item>

    <q-separator spaced inset />

    <q-item clickable v-ripple @click="card_2 = true">
      <q-item-section>
        <q-item-label lines="2">Realize 2 vendas maiores que R$ 50,00</q-item-label>
      </q-item-section>

      <q-item-section side top>
        0/2
      </q-item-section>
    </q-item>
  </q-list>
  <q-dialog v-model="nivel">
    <q-card class="my-card">
      <q-card-section>
        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            Seu Nível Atual: 1
          </div>
          <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            Nível 1
          </div>
        </div>
        <q-separator></q-separator>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          XP Atual: <strong>20/100</strong>
        </div>

      </q-card-section>

      <q-separator/>

      <q-card-section class="q-pt-none" style="margin-top: 20px; margin-bottom: 10px">
        <div class="text-subtitle1">
          Próximo Nível: <strong>Nível 2</strong>
        </div>
        <q-separator></q-separator>
        <div class="text-subtitle1" style="margin-top: 20px">
          Recompensas de próximo:
        </div>
        <div class="text-caption text-grey">
          1-Gráficos de Transações e Faturamento;
          <br>
          2 - Alertas de descontos em Milhos de Pipoca;
        </div>
        <q-card-actions align="center">
          <q-btn v-close-popup flat color="primary" label="Voltar" />
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>
  <q-dialog v-model="card">
    <q-card class="my-card">
      <q-card-section>
        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            Realize 5 vendas
          </div>
          <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            <q-icon name="place"/>
            Nível 1
          </div>
        </div>
        <q-separator></q-separator>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          Recompensas:
        </div>
        <div class="text-caption text-grey">
          1 - 10XP
        </div>
        <div class="text-caption text-grey">
          2 - Desconto de 5% em Milhos para Pipoca
        </div>
      </q-card-section>

      <q-separator/>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          Por que dessa missão:
        </div>
        <div class="text-caption text-grey">
          Atualmente seus concorrentes realizam em média 20 vendas.
        </div>
        <div class="text-caption text-grey">
          Você realiza em média 3.
        </div>
        <div id="chart">

        </div>
        <div class="text-subtitle1">
          Grafico aqui!
        </div>
        <q-card-actions align="center">
          <q-btn v-close-popup flat color="primary" label="Voltar" />
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>
  <q-dialog v-model="card_2">
    <q-card class="my-card">
      <q-card-section>
        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            Realize 2 vendas maiores que R$ 50,00
          </div>
          <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            <q-icon name="place"/>
            Nível 1
          </div>
        </div>
        <q-separator></q-separator>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          Recompensas:
        </div>
        <div class="text-caption text-grey">
          1 - 20XP
        </div>
      </q-card-section>

      <q-separator/>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          Por que dessa missão:
        </div>
        <div class="text-caption text-grey">
          Atualmente seus concorrentes realizam vendas no valor de R$ 120,00
          (<span style="text-decoration: underline;">ticket médio</span>).
          <q-tooltip class="bg-indigo" :offset="[10, 10]">
          O ticket médio representa o valor médio gasto nos pedidos: quanto maior for o valor, mais os clientes estão gastando nos pedidos.
        </q-tooltip>
        </div>
        <div class="text-caption text-grey">
          Você realiza vendas em média de R$ 32,00(<span style="text-decoration: underline;">ticket médio</span>).
          <q-tooltip class="bg-indigo" :offset="[10, 10]">
          O ticket médio representa o valor médio gasto nos pedidos: quanto maior for o valor, mais os clientes estão gastando nos pedidos.
        </q-tooltip>
        </div>
        <div class="text-subtitle1">
          Grafico aqui!
        </div>
        <q-card-actions align="center">
          <q-btn v-close-popup flat color="primary" label="Voltar" />
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>
  <q-dialog v-model="mission_complete">
    <q-card class="my-card">
      <q-card-section>
        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            Missão completa!
          </div>
          <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            <q-icon name="star" style="color: orange;"/>
          </div>
        </div>
        <q-separator></q-separator>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          Você completou a missão
        </div>
        <div class="text-caption text-grey">
          Realize Vendas 5/5
        </div>
      </q-card-section>

      <q-separator/>
      <q-card-section class="q-pt-none">
        <div class="text-subtitle1">
          Recompensas
        </div>
        <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            <span style="font-size: 2.1em"><q-icon name="verified" style="color: green;"/> 10XP</span>
        </div>
        <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            <span style="font-size: 2.1em"><q-icon name="paid" style="color: orange;"/> 5% Desconto em Milhos de
              Pipoca Yoki <span style="font-size: 0.5em">(1 compra)</span>
              </span>
        </div>
      </q-card-section>
      <q-card-section class="q-pt-none">
        <q-card-actions align="center">
          <q-btn v-close-popup flat color="primary" label="Voltar" />
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>
  <q-footer bordered class="bg-white text-primary">
    <q-tabs no-caps active-color="secondary" indicator-color="transparent" class="text-grey" v-model="tab">
      <q-route-tab
        icon="rule"
        style="color:#FF6633"
        to="/"
        exact
      />
      <q-route-tab
        icon="hotel_class"
        style="color:#FF6633"
        to="/conquistas"
        exact
      />
      <q-route-tab
        icon="analytics"
        style="color:#FF6633"
        to="/graficos"
        exact
      />
      <q-route-tab
        icon="notifications_active"
        style="color:#FF6633"
        to="/alertas"
        exact
      />
    </q-tabs>
  </q-footer>
</template>
<script>
import { ref } from 'vue'
import ApexCharts from 'apexcharts'

export default {
  data () {
    const options = {
      chart: {
        type: 'line'
      },
      series: [{
        name: 'sales',
        data: [30, 40, 35, 50, 49, 60, 70, 91, 125]
      }],
      xaxis: {
        categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999]
      }
    }

    const chart = new ApexCharts(document.querySelector('#chart'), options)

    chart.render()
  },
  setup () {
    return {
      card: ref(false),
      card_2: ref(false),
      nivel: ref(false),
      mission_complete: ref(false),
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'
    }
  }
}
</script>
<style lang="sass" scoped>
  .my-card
    width: 100%
    max-width: 250px
</style>
