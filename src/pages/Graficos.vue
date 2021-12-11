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
        <q-item-label><q-badge style="background-color:#FF6633" text-color="white" label="40/100 XP" /></q-item-label>
      </q-item-section>
      <q-item-section side top style="margin-top:1em;margin-right:3em;">
          <q-icon name="arrow_forward_ios" style="color:#009933"/>
      </q-item-section>
    </q-item>
    <q-dialog v-model="nivel">
      <q-card class="my-card" style="min-width: 350px">
        <q-card-section>
          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">
              Seu Nível Atual: 2
            </div>
            <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              Iniciante
            </div>
          </div>
          <q-separator></q-separator>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-subtitle1">
            XP Atual: <strong>40/100</strong>
          </div>

        </q-card-section>

        <q-separator/>

        <q-card-section class="q-pt-none" style="margin-top: 20px; margin-bottom: 10px">
          <div class="text-subtitle1">
            Próximo Nível: <strong>Nível 3</strong>
          </div>
          <q-separator></q-separator>
          <div class="text-subtitle1" style="margin-top: 20px">
            Recompensas de próximo:
          </div>
          <div class="text-caption text-grey">
            1 - Alertas de descontos em insumos;
          </div>
          <q-card-actions align="center">
            <q-btn v-close-popup flat color="deep-orange" label="Voltar" />
          </q-card-actions>
        </q-card-section>
      </q-card>
    </q-dialog>
    <q-list bordered class="rounded-borders" style="min-width: 350px;margin-top: 20px">
      <q-item-label header>Perfil do Estabelecimento</q-item-label>
          <q-carousel
            v-model="slide"
            transition-prev="scale"
            transition-next="scale"
            swipeable
            animated
            control-color="black"
            navigation
            padding
            arrows
            height="300px"
            class="shadow-1 rounded-borders"
          >
            <q-carousel-slide name="graph1" class="column no-wrap" style="padding:0px;">
              <div id="chartGraph">
              </div>
            </q-carousel-slide>
            <q-carousel-slide name="graph2" class="column no-wrap" style="padding:0px;">
              <div id="chartGraph2">
              </div>
            </q-carousel-slide>
          </q-carousel>
      <q-separator/>
      <q-item-label header style="background-color:gray; color: white">
        <div class="row">
          <q-icon name="lock" /><span style="font-size: 1em;margin-left:1em;">Perfil dos Consumidores - Nível 5</span>
        </div>
      </q-item-label>
      <q-item-label header style="background-color:gray; color: white">
        <div class="row">
          <q-icon name="lock" /><span style="font-size: 1em;margin-left:1em;">Perfil da Região - Nível 8</span>
        </div>
      </q-item-label>
      <q-item-label header style="background-color:gray; color: white">
        <div class="row">
          <q-icon name="lock" /><span style="font-size: 1em;margin-left:1em;">Concorrência - Nível 15</span>
        </div>
      </q-item-label>
    </q-list>
    <q-footer bordered class="bg-white text-primary">
      <q-tabs no-caps active-color="secondary" indicator-color="transparent" class="text-grey" v-model="tab">
        <q-route-tab
          icon="home"
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
  </div>
</template>
<script>
import { ref } from 'vue'
import { Chart } from 'frappe-charts/dist/frappe-charts.min.esm'
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
  setup () {
    return {
      card: ref(false),
      card_2: ref(false),
      nivel: ref(false),
      fullscreen: ref(false),
      mission_complete: ref(false),
      charts: null,
      slide: ref('graph1'),
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'
    }
  },
  watch: {
    slide: function (val) {
      switch (val) {
        case 'graph1':
          this.loadGraph1()
          break
        case 'graph2':
          this.loadGraph2()
          break
        default:
          console('não tem!')
      }
    }
  },
  methods: {
    loadGraph1 () {
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
    }
  },
  mounted () {
    this.loadGraph1()
  }
}
</script>
<style lang="sass" scoped>
  .my-card
    width: 100%
    max-width: 250px
</style>
