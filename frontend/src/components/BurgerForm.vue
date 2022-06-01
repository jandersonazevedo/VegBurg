<template>
  <div>
    <p>Component de mensagem</p>
    <form id="burger-form">
      <div class="input-container">
        <label
          ><span>Nome do cliente:</span>
          <input
            type="text"
            name="nome"
            v-model="nome"
            placeholder="Digite o seu nome"
            required
          />
        </label>
      </div>
      <div class="input-container">
        <label
          ><span>Escolha o pão:</span>
          <select name="pao" v-model="pao" required>
            <option value="" selected>Selecione seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.type">
              {{ pao.tipo }}
            </option>
          </select>
        </label>
      </div>
      <div class="input-container">
        <label
          ><span>Escolha a carne: </span>
          <select name="carne" v-model="carne">
            <option value="" selected>Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </label>
      </div>
      <div class="input-container" id="opcionais-container">
        <label id="opcionais-title"
          ><span>Selecione os opcionais:</span>
        </label>
        <div
          class="container-checkbox"
          v-for="opcional in opcionaisdata"
          :key="opcional.id"
        >
          <label
            ><input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="opcional.tipo"
            />
            <span>{{ opcional.tipo }}</span>
          </label>
        </div>
      </div>
      <div class="input-container">
        <input type="submit" class="submit-btn" value="Fazer pedido" />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "BurgerForm",
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      status: "Solicitado",
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();
      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },
  },
  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: auto;
}

.input-container > label {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label > span,
span {
  font-weight: bold;
  margin-bottom: 15px;
  color: #111;
  padding: 5px 10px;
  border-left: 4px solid #00b050;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#opcionais-container {
  margin-top: 15px;
  flex-direction: row;
  flex-wrap: wrap;
  display: flex;
}

#opcionais-container > label {
  margin-bottom: 0px;
}

#opcionais-title {
  width: 100%;
}

.container-checkbox {
  display: flex;
  width: 50%;
  align-items: center;
  margin-bottom: 20px;
}

.container-checkbox > label > span,
.container-checkbox > label > input {
  width: auto;
}

.container-checkbox > label > span {
  margin-left: 6px;
  font-weight: bold;
  border: 0;
  padding: 0;
}

.submit-btn {
  background-color: #111;
  color: #00b050;
  border: 2px solid #111;
  padding: 10px 10px;
  font-weight: bold;
  cursor: pointer;
  font-size: 15px;
  margin: 0 auto;
  transition: 0.5s;
}

.submit-btn:hover {
  background-color: #00b050;
  color: #222;
}
</style>