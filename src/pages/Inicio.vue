<template>
<div class="q-pa-md q-gutter-md"></div>
    <q-item clickable v-ripple style="margin-top:3em;">
      <q-item-section side>
        <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar.png">
        </q-avatar>
      </q-item-section>
      <!-- <q-item-section side>
        <q-chip style="">JJ</q-chip>
      </q-item-section> -->
      <!-- <q-item-section side>
          <div class="q-pa-md q-gutter-md">
            <q-badge rounded color="grey" label="JJ" />
          </div>
      </q-item-section> -->
      <q-item-section>
        <q-item-label>Olá, Jozias <q-avatar icon="arrow_forward_ios" color="white" text-color="orange" /></q-item-label>
      </q-item-section>
    </q-item>
    <div style="margin-top:2em;">
        <div class="row justify-center">
            <div class="row">
                <div>Saldo</div>
            </div>
        </div>
        <div class="row justify-center">
            <div class="row">
                <div>0,07</div>
            </div>
        </div>
        <div class="row justify-center">
            <div class="row">
                <div style="color:orange;">Adicionar dinheiro</div>
            </div>
        </div>
    </div>
    <q-separator style="margin:3em;5em;3em;0em;"/>
    <span style="color:green;margin-left:2em;">
        A receber
    </span>
    <div class="row justify-center q-pa-md q-gutter-md">
        <q-btn round color="deep-orange" icon="qr_code_scanner" />
        <q-btn round color="deep-orange" glossy icon="table_chart" />
        <q-btn round color="deep-orange" icon="payments" />
        <q-btn round color="deep-orange" icon="paid" />
    </div>
    <div class="row justify-center q-pa-md q-gutter-sm">
        <q-btn color="white" text-color="orange" icon="credit_card" icon-right="arrow_forward_ios" label="Cartão de crédito" />
    </div>
    <div class="row justify-center q-pa-md q-gutter-sm">
        <q-btn color="white" text-color="orange" icon="psychology" icon-right="arrow_forward_ios" label="Inteligência dos Deugis" />
    </div>
    <div class="row" style="margin-top:2em;">
       <div class="text-h6">Atividades Recentes</div>
    </div>
    <div class="row">
        Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum. 
    </div>
</template>
<script>
export default {
  setup () {
    return {
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
