<template>
  <div id="UserBalance">
    <div id="container">
      <h2>Tu saldo es:</h2>
      <p :class="{ hide: isActive }">
        <span> {{ balance }} COP </span>
      </p>
      <div id="seleccion-ingreso" class="select" @change="mostrarIngreso">
        <select name="ingreso" id="ingreso" v-model="seleccionado">
          <option value="" disabled>Seleccione un ingreso</option>
          <option value="salario" selected>Salario</option>
          <option value="ocasional">Ocasional</option>
          <option value="inversion">Inversión</option>
        </select>
      </div>
      <img src="../assets/save_money.svg" alt="" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "UserBalance",
  data: function () {
    return {
      balance: 0,
      seleccionado: "",
      isActive: true,
    };
  },
  methods: {
    mostrarIngreso() {
      this.isActive = false;
      axios
        .get(`http://127.0.0.1:8000/user/ingresos/${this.seleccionado}`)
        .then((res) => (this.balance = res.data.valor))
        .catch((error) => console.error(error));
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:ital,wght@1,300&display=swap");

#UserBalance {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #000000; 
}

#container {
  width: 400px;
  height: 400px;
  background-color: #D5DBDB;
  border-radius: 16px;
  border: 2px solid white;
  text-align: center;
  font-family: 'Roboto', sans-serif;
  display: flex;
  align-items: center;
  flex-direction: column;
}
#UserBalance h2 {
  font-size: 50px;
  color: #283747;
  padding: 0;
  margin: 30px 0 0 0;
}
span {
  color: crimson;
  font-weight: bold;
  font-size: 30px;
  background-image: url(../assets/save_money.svg);
}
img {
  width: 150px;
  height: 150px;
}
select {
  /* Additional resets for further consistency */
  appearance: none;
  background-color: transparent;
  border: none;
  padding: 0 1em 0 0;
  margin: 0;
  width: 100%;
  font-family: inherit;
  font-size: inherit;
  cursor: inherit;
  line-height: inherit;
}

.select {
  width: 150px;
  height: 20px;
  border-radius: 16px;
  padding: 1rem 1.5rem;
  border: 1px solid #000;
  font-size: 13px;
  line-height: 28px;
  color: #000;
  cursor: pointer;
  background-color: #fff;
  background-image: url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23007CB2%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E"),
    linear-gradient(to bottom, #ffffff 0%, #f7f7f7 100%);
  background-repeat: no-repeat, repeat;
  background-position: right 1.5em top 50%, 0 0;
  background-size: 0.65em auto, 100%;
  filter: drop-shadow(0px 5px 0px #18191f);
}
select:focus {
  outline: none;
}
.hide {
  opacity: 0;
}
</style>