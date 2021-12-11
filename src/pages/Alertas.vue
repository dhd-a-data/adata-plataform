<template>
  <div>
    <q-dialog v-model="alerta" position="top">
      <q-banner style="background-color:#009933;" class="text-white">
        Oportunidade! O preço do insumo "Milho para Pipoca Yoki" baixou. Valor atual R$ 1,85.
        <template v-slot:action>
          <a href="//www.atacadao.com.br" target="_blank" style="text-decoration:none">
            <q-btn flat color="white" label="Acessar"/>
          </a>
          <q-btn flat color="white" label="Fechar" @click="alerta = false" />
        </template>
      </q-banner>
    </q-dialog>
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
    <q-list style="margin-top:2em;">
        <div v-show="notification">
          <q-item >
            <q-item-section>
              <q-item-label>Oportunidade</q-item-label>
              <q-item-label caption>Aproveite a baixa do preço do insumo "Milho de Pipoca Yoki" por R$ 1,85 .</q-item-label>
            </q-item-section>

            <q-item-section side top>
              <q-item-label caption>agora</q-item-label>

              <q-icon name="attach_money" style="color: darkgreen" />

            </q-item-section>
          </q-item>

          <q-separator spaced inset />
        </div>

        <q-item>
          <q-item-section>
            <q-item-label>Você alcançou o Nível 2</q-item-label>
            <q-item-label caption lines="2">Parabéns você passou de nível e desbloqueou recompensas.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min atrás</q-item-label>
            <q-icon name="star" color="yellow" />
          </q-item-section>
        </q-item>

        <q-separator spaced inset />

        <q-item>
          <q-item-section>
            <q-item-label>Novo Gráfico liberado!</q-item-label>
            <q-item-label caption>Você liberou o gráfico de Perfil de estabelecimento, confira!</q-item-label>

          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min atrás</q-item-label>
            <q-icon name="analytics" color="blue" />
          </q-item-section>
        </q-item>

        <q-separator spaced inset />

        <q-item>
          <q-item-section>
            <q-item-label>Você completou uma missão</q-item-label>
            <q-item-label caption>Você completou a missão "Realize 5 vendas" e ganhou 10XP.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-badge color="teal" label="10XP" />
          </q-item-section>
        </q-item>

        <q-separator spaced inset />

        <q-item>
          <q-item-section>
            <q-item-label>Você ingressou no Parceirão</q-item-label>
            <q-item-label caption>Seja bem vindo, agora você faz parte do programa de ...</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>10/12/2021</q-item-label>
            <q-icon name="flag_circle" style="color: steelblue" />
          </q-item-section>
        </q-item>
      </q-list>
    <q-dialog v-model="nivel">
      <q-card class="my-card" style="min-width: 350px">
        <q-card-section>
          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis" style="color:#FF6633">
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
      alerta: ref(false),
      card: ref(false),
      card_2: ref(false),
      nivel: ref(false),
      notification: ref(false),
      mission_complete: ref(false),
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'
    }
  },
  mounted () {
    setTimeout(() => {
      this.alerta = true
      this.notification = true
    }, 5000)
  }
}
</script>
<style lang="sass" scoped>
  .my-card
    width: 100%
    max-width: 250px
</style>
