<template>
  <div class="burger-container">
    <Message :msg="msg" v-show="msg" />
    <form id="burger-form" @submit="createHamburger">
      <div class="input-container">
        <label for="name">Nome do client:</label>
        <input 
          type="text" 
          id="name"  
          v-model="nome" 
          placeholder="Digite o seu nome"
        >
      </div>
      <div class="input-container">
        <label for="pao">Escolha o pão:</label>
        <select id="pao" v-model="pao">
          <option value="">Selecione o tipo de pão</option>  
          <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
            {{ pao.tipo }}
          </option>
        </select>
      </div>
      <div class="input-container">
        <label for="carne">Escolha a carne:</label>
        <select id="carne" v-model="carne">
          <option value="">Selecione o tipo de carne</option>  
          <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
            {{ carne.tipo }}
          </option>
        </select>
      </div>
      <div id="opcionais-container" class="input-container">
        <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
        <div 
          class="chekbox-container" 
          v-for="opcional in opcionaisdata" 
          :key="opcional.id"
          >
          <input type="checkbox" v-model="opcionais" id="opcionais" :value="opcional.tipo">
          <span>{{ opcional.tipo }}</span>
        </div>
      </div>
      <div class="input-container">
        <ButtonModel value="Criar o seu Hamburger" />
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import Message from './Message.vue'
import ButtonModel from './Button.vue'

export default {
  name: "BurgerForm",
  components: {
    Message,
    ButtonModel
  },
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: '',
      carne: '',
      opcionais: [],
      status: 'Solicitado',
      msg: null
    }
  },
  methods: {
    async getIngredients() {
      await axios.get('http://localhost:3000/ingredientes')
        .then(res => {
          this.paes = res.data.paes
          this.carnes = res.data.carnes
          this.opcionaisdata = res.data.opcionais
        })
        .catch(err => console.error(err.data))
    },
    async createHamburger(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: 'Solicitado',
      }

      await axios.post('http://localhost:3000/burgers',data)
        .then(res => {
          this.msg = `Pedido Nº ${res.data.id} realizado com sucesso`
        })
        .catch(err => console.error(err.message))

        
      this.nome = ''
      this.pao = ''
      this.carne = ''
      this.opcionais = ''
      
      setTimeout(() => {
        this.msg = ''
      },3000)
    }
  },
  mounted() {
    this.getIngredients()
  }
}
</script>

<style scoped lang="scss">
  #burger-form {
    max-width: 18.5rem;
    margin: 0 auto;
    display: flex;
    flex-direction: column;

    .input-container {
      display: flex;
      flex-direction: column;
      margin-bottom: 1.2rem;
      
      label {
        padding: .3rem .5rem;
        color: #222;
        font-weight: bold;
        border-left: .2rem solid #fcba03;
        margin-bottom: .5rem;
      }
      
      input, select {
        padding: .3rem .5rem;
        width: 18.5rem;
      }
    }

    #opcionais-container {
      flex-direction: row;
      flex-wrap: wrap;

      .chekbox-container {
        display: flex;
        align-items: center;
        gap: .5rem;
        width: 50%;
        margin-bottom: 1.2rem;

        span, input {
          width: auto;
        }

        span {
          font-weight: bold;
        }

        input {
          cursor: pointer;
        }
      }
    }
  }
</style>