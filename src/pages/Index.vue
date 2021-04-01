<template>
  <q-page class="bg-dark">
    <div class="full-width" style="height:10px"></div>

    <div class="full-width" style="height: 15vh">
      <q-card bordered class="q-mx-auto" style="width: 95vw; height: 25vh">
        <q-card-section class="row justify-between">
          <div class="text-subtitle1 text-grey-6">Entradas</div>
          <q-img
            src="https://raw.githubusercontent.com/rocketseat-education/maratona-discover-01/9d0b7435ded694abeba1e932c1f9b3f263fecbff/assets/income.svg"
            spinner-color="white"
            style="height: 35px; width: 35px"
          />
        </q-card-section>

        <q-card-section class="text-h5 text-primary">
          R$ 5000
        </q-card-section>
      </q-card>

      <q-card
        bordered
        class="q-mx-auto q-my-sm"
        style="width: 95vw; height: 25vh"
      >
        <q-card-section class="row justify-between">
          <div class="text-subtitle1 text-grey-6">Saídas</div>
          <q-img
            src="https://raw.githubusercontent.com/rocketseat-education/maratona-discover-01/9d0b7435ded694abeba1e932c1f9b3f263fecbff/assets/expense.svg"
            spinner-color="white"
            style="height: 35px; width: 35px"
          />
        </q-card-section>

        <q-card-section class="text-h5 text-primary">
          R$ 3000
        </q-card-section>
      </q-card>

      <q-card
        bordered
        class="q-mx-auto bg-secondary"
        style="width: 95vw; height: 25vh"
      >
        <q-card-section class="row justify-between">
          <div class="text-subtitle1 text-primary">Total</div>
          <q-img
            src="https://raw.githubusercontent.com/rocketseat-education/maratona-discover-01/9d0b7435ded694abeba1e932c1f9b3f263fecbff/assets/total.svg"
            spinner-color="white"
            style="height: 35px; width: 35px;"
          />
        </q-card-section>

        <q-card-section class="text-h5 text-grey-2">
          R$ 2000
        </q-card-section>
      </q-card>

      <div class="text-h5 row q-my-md items-center justify-center">
        <q-separator style="width: 28vw" color="primary" />
        <div class="q-px-sm text-primary">Registros</div>
        <q-separator style="width: 28vw" color="primary" />
      </div>

      <q-scroll-area class="bg-dark full-width q-mb-xl" style="height: 300px;">
        <q-card
          v-for="(registro, index) in registros"
          :key="index"
          bordered
          class="q-mx-auto bg-secondary q-my-sm"
          style="width: 95vw;"
        >
          <q-card-section class="row justify-between items-center">
            <div class="text-subtitle1 text-primary">
              {{ registro.descricao }}
            </div>
            <div class="text-subtitle1 text-primary">
              R${{ registro.valor }}
            </div>
            <div class="text-subtitle1 text-primary">{{ registro.data }}</div>
            <q-img
              src="https://raw.githubusercontent.com/rocketseat-education/maratona-discover-01/9d0b7435ded694abeba1e932c1f9b3f263fecbff/assets/minus.svg"
              spinner-color="white"
              style="height: 20px; width: 20px;"
              @click="deleteRegistro(registro.id)"
            />
          </q-card-section>
        </q-card>
      </q-scroll-area>

      <footer class="bg-dark row justify-center q-py-lg">
        <q-img
          src="https://raw.githubusercontent.com/rocketseat-education/maratona-discover-01/9d0b7435ded694abeba1e932c1f9b3f263fecbff/assets/logo.svg"
          style="height: 20px; width: 150px"
        />
      </footer>

      <q-page-sticky position="bottom-right" :offset="[18, 18]">
        <q-btn fab icon="add" color="green-6" @click="dialogCadastro = true" />
      </q-page-sticky>

      <q-dialog
        v-model="dialogCadastro"
        persistent
        :maximized="maximizedToggle"
        transition-show="slide-up"
        transition-hide="slide-down"
      >
        <q-card class="bg-primary text-white">
          <q-bar>
            <q-space />
          </q-bar>

          <q-card-section>
            <div class="text-h6">Novo registro</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            <q-input filled v-model="registro.descricao" label="Descrição" />
            <q-input
              class="q-my-sm"
              type="number"
              filled
              v-model="registro.valor"
              label="Valor"
            />
            <q-input
              filled
              mask="##/##/##"
              v-model="registro.data"
              label="Data"
            />
          </q-card-section>

          <q-card-actions class="full-width justify-center">
            <q-btn
              outline
              color="white"
              label="Fechar"
              style="width: 46%"
              v-close-popup
            />
            <q-btn
              color="secondary"
              label="Salvar"
              style="width: 46%"
              v-close-popup
              @click="addRegistro"
            />
          </q-card-actions>
        </q-card>
      </q-dialog>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      dialogCadastro: false,
      maximizedToggle: true,
      registro: {
        descricao: '',
        valor: 0,
        data: ''
      },
      registros: []
    }
  },
  methods: {
    addRegistro () {
      const vm = this
      this.$axios
        .post('http://172.22.4.80:1337/registros', {
          descricao: vm.registro.descricao,
          valor: vm.registro.valor,
          data: vm.registro.data,
          tipo: null
        })
        .then(res => {
          vm.notificacao('Registro inserido com sucesso', 'positive', 'top')
          window.location.reload()
        })
        .catch(() => {
          vm.notificacao('Erro ao inserir registro', 'negative', 'top')
        })
    },

    getRegistros () {
      const vm = this
      this.$axios
        .get('http://172.22.4.80:1337/registros', {})
        .then(function (res) {
          vm.registros = res.data
          // vm.notificacao('Carregou os dados', 'positive', 'top')
        })
        .catch(function () {
          vm.notificacao('Erro ao carregar dados', 'negative', 'top')
        })
    },

    deleteRegistro (id) {
      const vm = this
      vm.notificacao('Erro ao deletar registro', 'negative', 'top')
      this.$axios
        .delete(`http://172.22.4.80:1337/registros/${id}`, {})
        .then(function () {
          vm.notificacao('Registro deletado', 'positive', 'top')
          window.location.reload()
        })
        .catch(function (error) {
          console.log('ERRO', error)
          vm.notificacao('Erro ao deletar registro', 'negative', 'top')
        })
    },

    notificacao (mensagem, tipo, posicao) {
      this.$q.notify({
        message: mensagem,
        type: tipo,
        position: posicao
      })
    }
  },
  mounted () {
    this.getRegistros()
  }
}
</script>
