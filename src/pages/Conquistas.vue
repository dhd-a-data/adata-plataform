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
        <q-item-label><q-badge style="background-color:#FF6633" text-color="white" label="10/100 XP" /></q-item-label>
      </q-item-section>
      <q-item-section side top style="margin-top:1em;margin-right:3em;">
          <q-icon name="arrow_forward_ios" style="color:#009933"/>
      </q-item-section>
    </q-item>
    <div class="row justify-center">
      <q-list bordered class="rounded-borders" style="width: 100%;margin-top: 20px">
        <q-item-label header>Conquistas</q-item-label>
        <q-separator spaced />
        <q-item clickable v-ripple @click="card = true">
          <q-item-section>
            <q-item-label lines="1">Realize 5 vendas</q-item-label>
            <q-item-label caption lines="2">
            </q-item-label>
          </q-item-section>
          <q-item-section side top>
            <q-icon name="done" color="green-7"></q-icon>
          </q-item-section>
        </q-item>
      </q-list>
    </div>
    <q-dialog v-model="nivel">
      <q-card class="my-card" style="min-width: 350px">
        <q-card-section>
          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">
              Seu Nível Atual: 1
            </div>
            <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              Iniciante
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

export default {
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
