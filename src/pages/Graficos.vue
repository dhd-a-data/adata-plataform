<template>
  <div class="q-pa-md q-gutter-md"></div>
  <q-item clickable v-ripple style="margin-top:3em;">
    <q-item-section side>
      <q-avatar>
        <img src="~assets/pipoqueiro.png">
      </q-avatar>
    </q-item-section>
    <q-item-section @click="nivel = true">
      <q-item-label>Olá, João Pipoqueiro</q-item-label>
      <q-item-label>Nivel 1 - 20/100 XP</q-item-label>
    </q-item-section>
  </q-item>
  <q-list bordered class="rounded-borders" style="max-width: 350px;margin-top: 20px">
    <q-item-label header>Perfil do Estabelecimento Nível 2</q-item-label>
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
    <q-item-label header style="background-color:gray; color: white">Perfil dos Consumidores
      <span style="font-size: 0.8em">Nível 5</span></q-item-label>
    <q-item-label header style="background-color:gray; color: white">Perfil da Região
      <span style="font-size: 0.8em">Nível 8</span></q-item-label>
    <q-item-label header style="background-color:gray; color: white">Concorrência
      <span style="font-size: 0.8em">Nível 15</span></q-item-label>
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
</template>
<script>
import { ref } from 'vue'
import { Chart } from 'frappe-charts/dist/frappe-charts.min.esm'
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
      console.log('verificando slide: ', this.slide)
      setTimeout(() => {
        // eslint-disable-next-line no-unused-vars
        this.charts = new Chart('#chartGraph', {
          title: 'My Awesome Chart',
          data: data,
          type: 'axis-mixed', // or 'bar', 'line', 'scatter', 'pie', 'percentage'
          height: 250,
          colors: ['#FF6633', '#009933'],
          lineOptions: {
            dotSize: 6 // default: 4
          }
        })
        this.$q.loading.hide()
      }, 500)
    },
    loadGraph2 () {
      console.log('verificando slide: ', this.slide)
      setTimeout(() => {
        // eslint-disable-next-line no-unused-vars
        const charts2 = new Chart('#chartGraph2', {
          title: 'Grafico 2',
          data: data,
          type: 'axis-mixed', // or 'bar', 'line', 'scatter', 'pie', 'percentage'
          height: 250,
          colors: ['#7cd6fd', '#743ee2'],
          lineOptions: {
            dotSize: 6 // default: 4
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
