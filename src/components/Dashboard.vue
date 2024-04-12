<template>
  <div class="burger-table">
    <Message :msg="msg" v-show="msg" />
    <table class="basic">
      <thead>
        <tr>
          <th class="id">Id:</th>
          <th>Cliente:</th>
          <th>Pão:</th>
          <th>Carne:</th>
          <th>Opcionais:</th>
          <th>Ações:</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="burger in burgers" :key="burger.id">
          <td>{{ burger.id }}</td>
          <td>{{ burger.nome }}</td>
          <td>{{ burger.pao }}</td>
          <td>{{ burger.carne }}</td>
          <td>
            <ul>
              <li v-for="(opcional,index) in burger.opcionais" :key="index">
                {{ opcional }}
              </li>
            </ul>
          </td>
          <td>
            <div class="select">
              <select 
                name="status" 
                class="status"
                
                @change="updateBurger($event,burger.id)" 
              >
                <option value="">Selecione o status do Hamburger</option>
                <option v-for="stat in status" :selected="burger.status === stat.tipo" :key="stat.id" :value="stat.tipo">
                  {{ stat.tipo }}
                </option>
              </select>
              <ButtonModel @click="cancelPedido(burger.id)" value="Cancelar" />
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
import ButtonModel from './Button.vue'
import Message from './Message.vue'

export default {
  name: "Dashboard",
  components: { 
    ButtonModel,
    Message 
  },
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null,
    }
  },
  methods: {
    async getPedidos() {
      await axios.get('http://localhost:3000/burgers')
        .then(res => {
          this.burgers = res.data
        })
        .catch(err => console.error(err.message))

      this.getStatus()
      
    },
    async getStatus() {
      await axios.get('http://localhost:3000/status')
        .then(res => {
          this.status = res.data
        })
        .catch(err => console.error(err.message))
    },
    async cancelPedido(id) {
      await axios.delete(`http://localhost:3000/burgers/${id}`)
        .then(res => {
          this.msg = `O pedido Nº ${res.data.id} foi Cancelado`
        })
        .catch(err => console.error(err.message))

      this.getPedidos()

      setTimeout(() => {
        this.msg = null
      },3000)

    },
    async updateBurger(ev, id) {
      const data = {status: ev.target.value}

      await axios.patch(`http://localhost:3000/burgers/${id}`, data)
        .then(res => {
          this.msg = `O pedido Nº ${res.data.id} 
            foi actualizado para "${res.data.status}"`
        })
        .catch(err => console.error(err.message))

      setTimeout(() => {
        this.msg = null
      },3000)
    }
  },
  mounted() {
    this.getPedidos()
  }
}
</script>

<style scoped lang="scss">
  .burger-table {
    max-width: 75rem;
    margin: 0 auto;
    overflow: auto;

    .basic {
      border-spacing: 0;
      td, th {
        padding: 0.6rem;
      }

      thead th {
        border-bottom: .2rem solid #333;
        width: 19%;
        text-align: left;
      }

      thead .id {
        width: 5%;
      }

      tbody {
        
        td {
          border-bottom: .1rem solid #ccc;

          .select {
            display: flex;
            gap: .5rem;

            select {
              padding: .6rem .3rem;
              width: 6rem;
            }  
          }
        }
      }
    }
  }
</style>