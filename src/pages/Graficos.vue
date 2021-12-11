<template>
  <div class="q-pa-md q-gutter-md"></div>
  <q-item clickable v-ripple style="margin-top:3em;">
    <q-item-section side>
      <q-avatar>
        <img src="https://cdn.quasar.dev/img/avatar.png">
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
          swipeable
          animated
          arrows
          v-model="slide"
          v-model:fullscreen="fullscreen"
          infinite
        >
          <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg"/>
          <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg"/>
          <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg"/>
          <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg"/>

          <template v-slot:control>
            <q-carousel-control
              position="bottom-right"
              :offset="[18, 18]"
            >
              <q-btn
                push round dense color="white" text-color="primary"
                :icon="fullscreen ? 'fullscreen_exit' : 'fullscreen'"
                @click="fullscreen = !fullscreen"
              />
            </q-carousel-control>
          </template>
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
    <q-tabs no-caps active-color="primary" indicator-color="transparent" class="text-grey" v-model="tab">
      <q-tab name="images" label="Missões" @click=" mission_complete = true"/>
      <q-route-tab
        label="Conquistas"
        to="/"
        exact
      />
      <q-route-tab
        label="Gráficos"
        to="/graficos"
        exact
      />
      <q-route-tab
        label="Notificações"
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

    var chart = new ApexCharts(document.querySelector('#chart'), options)

    chart.render()
  },
  setup () {
    return {
      card: ref(false),
      card_2: ref(false),
      nivel: ref(false),
      slide: ref(1),
      fullscreen: ref(false),
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
