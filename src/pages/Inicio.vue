<template>
  <div>
    <q-item clickable v-ripple>
      <q-item-section side>
        <q-avatar size="50px">
          <img src="~assets/pipoqueiro.png">
        </q-avatar>
      </q-item-section>
      <q-item-section @click="nivel = true">
        <q-item-label>Olá, <span class="text-weight-medium">João Pipoqueiro</span></q-item-label>
        <q-item-label><q-badge style="background-color:#FF6633" text-color="white" :label="xpLabel" /></q-item-label>
      </q-item-section>
      <q-item-section side top style="margin-top:1em;margin-right:3em;">
          <q-icon name="arrow_forward_ios" style="color:#009933"/>
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
    <div class="row justify-center">
      <q-list bordered class="rounded-borders" style="width: 100%; margin-top: 20px">
        <q-item-label header>Missões</q-item-label>
        <q-separator spaced />
        <div v-show="showProgress">
          <div clickable @click="loadGraph1">
          <q-item>
            <q-item-section>
              <q-item-label lines="1">Realize 5 vendas em um único dia</q-item-label>
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
        </div>
        <div @click="loadGraph2">
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
    </div>
    <q-dialog v-model="nivel">
      <q-card class="my-card" style="min-width: 350px">
        <q-card-section>
          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">
              Seu Nível Atual: {{ lvLabel }}
            </div>
            <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              Iniciante
            </div>
          </div>
          <q-separator></q-separator>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-subtitle1">
            XP Atual: <strong>{{ xpLabel }}</strong>
          </div>

        </q-card-section>

        <q-separator/>

        <q-card-section class="q-pt-none" style="margin-top: 20px; margin-bottom: 10px">
          <div class="text-subtitle1">
            Próximo Nível: <strong>Nível {{ lvLabel + 1}}</strong>
          </div>
          <q-separator></q-separator>
          <div class="text-subtitle1" style="margin-top: 20px">
            Recompensas de próximo:
          </div>
          <div class="text-caption text-grey">
            1 - Gráficos de Transações e Faturamento;
            <br>
            2 - Alertas de descontos em Milhos de Pipoca;
          </div>
          <q-card-actions align="center">
            <q-btn v-close-popup flat color="deep-orange" label="Voltar" />
          </q-card-actions>
        </q-card-section>
      </q-card>
    </q-dialog>
    <q-dialog v-model="card">
      <q-card class="my-card" style="max-width: 1500px;width:1000px;">
        <q-card-section>
          <div class="row no-wrap items-center">
            <q-item style="padding-left:0px;">
              <q-item-section>
                <q-item-label style="font-size:1.5em;" lines="2">Realize 5 vendas em um único dia</q-item-label>
              </q-item-section>
            </q-item>
            <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              <q-icon name="star"/>
              Iniciante
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
            <q-btn v-close-popup flat color="deep-orange" label="Voltar" />
          </q-card-actions>
        </q-card-section>
      </q-card>
    </q-dialog>
    <q-dialog v-model="card_2">
      <q-card class="my-card" style="min-width: 350px">
        <q-card-section>
          <div class="row no-wrap items-center">
            <q-item style="padding-left:0px;">
              <q-item-section>
                <q-item-label style="font-size:1.5em;" lines="2">Realize 2 vendas maiores que R$ 50,00</q-item-label>
              </q-item-section>
              <q-tooltip class="bg-green-5" :offset="[10, 10]">
                Realize 2 vendas maiores que R$ 50,00
              </q-tooltip>
            </q-item>
            <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              <q-icon name="place"/>
              Iniciante
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
            <q-tooltip class="bg-green-5" :offset="[10, 10]">
            O ticket médio representa o valor médio gasto nos pedidos: quanto maior for o valor, mais os clientes estão gastando nos pedidos.
          </q-tooltip>
          </div>
          <div class="text-caption text-grey">
            Você realiza vendas em média de R$ 32,00(<span style="text-decoration: underline;">ticket médio</span>).
            <q-tooltip class="bg-green-5" :offset="[10, 10]">
            O ticket médio representa o valor médio gasto nos pedidos: quanto maior for o valor, mais os clientes estão gastando nos pedidos.
          </q-tooltip>
          </div>
          <div class="text-subtitle1">
            <div id="chartGraph2">
            </div>
          </div>
          <q-card-actions align="center">
            <q-btn v-close-popup flat color="deep-orange" label="Voltar" />
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
              <q-icon size="25px" name="star" style="color: orange;padding-bottom:0.7em;"/>
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
              <span style="font-size: 1.1em"><q-icon name="verified" style="color: green;"/> 10XP</span>
          </div>
          <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              <span style="font-size: 1.1em"><q-icon name="paid" style="color: orange;"/> 5% Desconto em Milhos de
                Pipoca Yoki <span style="font-size: 0.7em">(1 compra)</span>
                </span>
          </div>
        </q-card-section>
        <q-card-section class="q-pt-none">
          <q-card-actions align="center">
            <q-btn v-close-popup flat color="deep-orange" label="Ok" />
          </q-card-actions>
        </q-card-section>
      </q-card>
    </q-dialog>
    <q-footer bordered class="bg-white text-primary">
      <q-tabs no-caps active-color="secondary" indicator-color="transparent" class="text-grey" v-model="tab">
        <q-tab name="images" icon="home" style="color:#44B1A7"/>
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
  </div>
</template>
<script>
import { ref } from 'vue'
import { Chart } from 'frappe-charts/dist/frappe-charts.min.esm'
import { QSpinnerFacebook } from 'quasar'

const data = {
  labels: ['04/12', '05/12', '06/12', '07/12',
    '08/12', '09/12', '10/12', '11/12'
  ],
  datasets: [
    {
      name: 'Você',
      type: 'bar',
      values: [4, 0, 3, 1, 4, 4, 2, 1]
    },
    {
      name: 'Concorrentes',
      type: 'line',
      values: [12, 8, 11, 13, 12, 10, 9, 11]
    }
  ]
}

const data2 = {
  labels: ['04/12', '05/12', '06/12', '07/12',
    '08/12', '09/12', '10/12', '11/12'
  ],
  datasets: [
    {
      name: 'Você',
      type: 'bar',
      values: [15, 12, 16, 8, 11, 10, 9, 10]
    },
    {
      name: 'Concorrentes',
      type: 'bar',
      values: [38, 45, 29, 15, 22, 29, 30, 21]
    }
  ]
}

export default {
  data () {
    return {
      lvLabel: 1,
      progressLabel1: '4/5'
    }
  },
  setup () {
    const progress1 = ref(0.8)
    const progress2 = ref(0.5)
    const showProgress = ref(true)
    return {
      card: ref(false),
      card_2: ref(false),
      nivel: ref(false),
      mission_complete: ref(false),
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
      progress1,
      progress2,
      progressLabel2: '1/2',
      value: 75,
      charts: null,
      xpLabel: '30/40 XP',
      hideProgress: true,
      showProgress
    }
  },
  methods: {
    loadGraph1 () {
      this.card = true
      this.message('Carregando...')
      setTimeout(() => {
        // eslint-disable-next-line no-unused-vars
        this.charts = new Chart('#chartGraph', {
          title: 'Quantidade de vendas por dia',
          data: data,
          type: 'axis-mixed', // or 'bar', 'line', 'scatter', 'pie', 'percentage'
          height: 250,
          colors: ['#009933', '#FF6633'],
          lineOptions: {
            dotSize: 8, // default: 4
            regionFill: 1 // default: 0
          }
        })
        this.$q.loading.hide()
      }, 500)
    },
    loadGraph2 () {
      this.card_2 = true
      this.message('Carregando...')
      setTimeout(() => {
        // eslint-disable-next-line no-unused-vars
        const charts2 = new Chart('#chartGraph2', {
          title: 'Valor médio de transação',
          data: data2,
          nivel: ref(false),
          type: 'bar', // or 'bar', 'line', 'scatter', 'pie', 'percentage'
          height: 250,
          colors: ['#009933', '#FF6633'],
          lineOptions: {
            dotSize: 8 // default: 4
          }
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
      this.xpLabel = '40/100 XP'
      this.lvLabel = 2
      this.progressLabel1 = '5/5'
      this.progress1 = 1
      this.value = 0
      setTimeout(() => {
        this.showProgress = false
      }, 1000)
    }, 5000)
  }
}
</script>
<style lang='sass' scoped>
  .my-card
    width: 100%
    max-width: 250px
</style>
