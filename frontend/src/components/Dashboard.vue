<template>
  <div id="burger-table">
    <Message :msg="msg" v-show="msg" />
    <table>
      <thead>
        <th>Nº</th>
        <th>Cliente</th>
        <th>Pão</th>
        <th>Carne</th>
        <th>Opcionais</th>
        <th></th>
      </thead>
      <tbody>
        <tr v-for="burger in burgers" :key="burger.id">
          <td>{{ burger.id }}</td>
          <td>{{ burger.nome }}</td>
          <td>{{ burger.pao }}</td>
          <td>{{ burger.carne }}</td>
          <td>
            <ul>
              <li v-for="(opcional, index) in burger.opcionais" :key="index">
                {{ opcional }}
              </li>
            </ul>
          </td>
          <td>
            <select name="status" @change="updateBurger($event, burger.id)">
              <option value="">Status</option>
              <option
                v-for="s in status"
                :key="s.id"
                :value="s.tipo"
                :selected="burger.status == s.tipo"
              >
                {{ s.tipo }}
              </option>
            </select>
            <button @click="deleteBurger(burger.id)">Cancelar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Message from "./Message.vue";
export default {
  name: "Dashboard",
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null,
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();
      this.burgers = data;
      this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();
      this.status = data;
    },
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });
      const res = await req.json();

      this.msg = `Pedido cancelado com sucesso!`;

      setTimeout(() => (this.msg = ""), 3000);
      this.getPedidos();
    },
    async updateBurger(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option });
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      this.msg = `O pedido  Nº ${res.id} foi atualizado para ${res.status}!`;

      setTimeout(() => (this.msg = ""), 3000);
    },
  },
  mounted() {
    this.getPedidos();
  },
  components: { Message },
};
</script>

<style scoped>
table {
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
  border-collapse: collapse;
  text-align: left;
}

thead {
  font-weight: bold;
  border-bottom: 1px solid #222;
}

th {
  padding: 12px;
}

tr {
  border-bottom: 0.5px solid rgba(51, 51, 51, 0.377);
}

td {
  padding: 12px;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}

button {
  background: #b01a00;
  color: #fff;
  font-weight: bold;
  border: 2px solid #b01a00;
  padding: 10px;
  margin: 0 auto;
  cursor: pointer;
  border-radius: 4px;
  transition: 0.5s;
}

button:hover {
  background-color: #fff;
  color: #b01a00;
}
</style>