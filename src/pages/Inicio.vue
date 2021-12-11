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
      <q-item-label>Nivel 1 - 10/100 XP</q-item-label>
    </q-item-section>
  </q-item>
  <div class="row justify-center">
    <q-circular-progress
        show-value
        font-size="12px"
        :value="value"
        size="90px"
        :thickness="0.22"
        color="green-7"
        track-color="grey-3"
        class="q-ma-md "
      >
        <span style="text-align:center;font-size:15px;color:#FF6633" class="roboto-font">Nível <br><span style="font-size:30px;">{{ lvLabel }}</span></span>
    </q-circular-progress>
  </div>
  <q-list bordered class="rounded-borders" style="max-width: 350px; margin-top: 20px">
    <q-item-label header>Missões</q-item-label>
    <q-separator spaced />
    <div clickable @click="openDialog">
      <q-item>
        <q-item-section>
          <q-item-label lines="1">Realize 5 vendas</q-item-label>
          <q-item-label caption lines="2">
          </q-item-label>
        </q-item-section>
      </q-item>
      <div class="q-pa-md">
        <q-linear-progress size="25px" :value="progress1" color="green-7">
          <div class="absolute-full flex flex-center">
            <q-badge color="white" style="color:#FF6633" :label="progressLabel1" />
          </div>
        </q-linear-progress>
      </div>
    </div>
    <q-separator spaced inset />
    <div @click="card_2 = true">
      <q-item clickable>
        <q-item-section>
          <q-item-label lines="2">Realize 2 vendas maiores que R$ 50,00</q-item-label>
        </q-item-section>
      </q-item>
      <div class="q-pa-md">
        <q-linear-progress size="25px" :value="progress2" color="green-7" class="q-mt-sm">
          <div class="absolute-full flex flex-center">
            <q-badge color="white" style="color:#FF6633" :label="progressLabel2" />
          </div>
        </q-linear-progress>
      </div>
    </div>
  </q-list>
  <q-dialog v-model="nivel">
    <q-card class="my-card" style="min-width: 350px">
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
          XP Atual: <strong>10/100</strong>
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
    <q-card class="my-card" style="min-width: 350px">
      <q-card-section>
        <div class="row no-wrap items-center">
          <div class="col text-h6 ellipsis">
            Realize 5 vendas
          </div>
          <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
            <q-icon name="star"/>
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
        <div class="text-subtitle1">
          <div id="chartGraph">
          </div>
        </div>
        <q-card-actions align="center">
          <q-btn v-close-popup flat color="primary" label="Voltar" />
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>
  <q-dialog v-model="card_2">
    <q-card class="my-card" style="min-width: 350px">
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
    <q-card class="my-card" style="min-width: 350px">
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
      <q-tab name="images" icon="rule" style="color:#44B1A7"/>
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
import { ref, computed } from 'vue'
import { Chart } from 'frappe-charts/dist/frappe-charts.min.esm'
import { QSpinnerFacebook } from 'quasar'

const data = {
  labels: ['12am-3am', '3am-6pm', '6am-9am', '9am-12am',
    '12pm-3pm', '3pm-6pm', '6pm-9pm', '9am-12am'
  ],
  datasets: [
    {
      name: 'Some Data',
      type: 'bar',
      values: [25, 40, 30, 35, 8, 52, 17, -4]
    },
    {
      name: 'Another Set',
      type: 'line',
      values: [25, 50, -10, 15, 18, 32, 27, 14]
    }
  ]
}

export default {
  setup () {
    const progress1 = ref(0.2)
    const progress2 = ref(0.5)
    return {
      card: ref(false),
      card_2: ref(false),
      nivel: ref(false),
      mission_complete: ref(false),
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
      progress1,
      progressLabel1: computed(() => '2/5'),
      progress2,
      progressLabel2: computed(() => '1/1'),
      value: 10,
      lvLabel: 1,
      charts: null
    }
  },
  methods: {
    openDialog () {
      this.card = true
      this.message('Carregando...')
      setTimeout(() => {
        // eslint-disable-next-line no-unused-vars
        this.charts = new Chart('#chartGraph', {
          title: 'My Awesome Chart',
          data: data,
          type: 'axis-mixed', // or 'bar', 'line', 'scatter', 'pie', 'percentage'
          height: 250,
          colors: ['#7cd6fd', '#743ee2']
        })
        this.$q.loading.hide()
      }, 500)
    },
    message (message, spinner) {
      this.$q.loading.show({
        spinner: spinner || QSpinnerFacebook,
        message: message
      })
    }
  },
  mounted () {
    setTimeout(() => {
      this.mission_complete = true
    }, 5000)
  }
}
</script>
<style lang='sass' scoped>
  .my-card
    width: 100%
    max-width: 250px
</style>
