<template>
  <div id="User">
       
      <form method="post">
        <label for="ingreso" id="enunciado">Egreso:</label>
        <input type="text" name="valor" v-model="valor" />
        <label for="tipo" id="enunciado">Tipo de egreso:</label>

        <div id="seleccion-ingreso" class="select">
          <select name="ingreso" id="ingreso" v-model="seleccionado">
            <option value="" disabled>Seleccione un egreso</option>
            <option value="arriendo" selected>Arriendo</option>
            <option value="transporte">Transporte</option>
            <option value="ocio">Ocio</option>
          </select>
        </div>

        <input type="date" value="fecha" v-model="dia">

        <input type="button" value="Enviar" @click="putEgresos" class="botones" />
        <input
          type="button"
          value="Ver Egresos"
          @click="showEgresos"
          class="botones"
        />
      </form>
      <section v-if="mostrar === false">
        <div id="UserBalance">
          <div id="container">
            <h2>Tus egresos son:</h2>
           
            <ul>
                <li v-for="(gasto, index) in egresos">
                 <p> <span>VALOR:</span> {{ gasto.valor }} COP   <span>FECHA:</span> {{ gasto.fecha }}</p>
                </li>
              </ul>
              <p id="total-titulo">TOTAL:</p>
              <p id="total"> {{ total }} COP</p>
          </div>
        </div>
       
      </section>
        <img v-if="mostrar" src="../assets/ingresos.svg" alt="" id="img-egresos">
    
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "User",
  data: function () {
    return {
      seleccionado: "",
      valor: "",
      dia: "",
      mostrar:true,
      egreso: 0,
      egresos:[],
      total: 0
    };
  },
  computed:{
    fecha: function() {
      let fechas = new Date( Date.now()),
        dia = fechas.getDate(),
        agno = fechas.getFullYear(),
        mes = fechas.getMonth() + 1;
      return `${agno}-${mes}-${dia}`
    }
  },
  methods: {
    putEgresos() {
      axios
        .put("http://127.0.0.1:8000/user/egresos/", {
          tipo: this.seleccionado,
          valor: parseInt(this.valor),
          fecha: this.dia,
        })
        .then((res) => console.log(res))
        .catch((error) => console.error(error));
    },
    showEgresos() {
      this.total = 0
      this.mostrar = false
      axios
        .get(`http://127.0.0.1:8000/user/egresos/${this.seleccionado}`)
        .then((res) => {
          this.egresos =Array.from(res.data)

          this.egresos.forEach(el => {
            this.total += el.valor
          })
          console.log(this.egreso)
        })
        .catch((error) => console.error(error));
    },
    verFecha(){
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:ital,wght@1,300&display=swap");

#User {
  background: beige; /* fallback for old browsers */
  

  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  font-family: sans-serif;
}
form {
  padding: 0;
  border: 1px solid black;
  line-height: 28px;
  border-radius: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 400px;
  height: 520px;
  background-color: #83879D;
  color: #e5e7e9;
  font-family: "Ubuntu", sans-serif;
}
h1{
  margin: 7%;
}

input[type="text"] {
  border: 1px solid #999;
  border-radius: 0;

  -webkit-appearance: none;
}
input[name="valor"] {
  text-align: center;
  font-family: "Ubuntu", sans-serif;
  font-size: 15px;
  font-weight: bold;
}

input[name="valor"]:focus {
  outline: none;
}

input[type="text"] {
  width: 150px;
  height: 20px;
  border-radius: 16px;
  padding: 1rem 1.5rem;
  border: 1px solid #000;
  font-size: 14px;
  line-height: 28px;
  color: #000;
  cursor: pointer;
}

select,
input[type="date"] {
  /* Additional resets for further consistency */
  appearance: none;
  background-color: transparent;
  border: none;
  padding: 0 1em 0 0;
  width: 100%;
  font-family: inherit;
  font-size: inherit;
  cursor: inherit;
  line-height: inherit;
}
select:focus,
input[type="date"] {
  outline: none;
}
input[type="date"] {
  margin-top: 15px;
  width: 150px;
  height: 20px;
  border-radius: 16px;
  padding: 1rem 1.5rem;
  border: 1px solid #000;
  font-size: 15px;
  font-weight: bold;
  line-height: 28px;
  color: #000;
  cursor: pointer;
  background-color: #fff;
  filter: drop-shadow(0px 5px 0px #18191f);
  text-align: center;

}

#User .select{
  width: 150px;
  height: 20px;
  border-radius: 16px;
  padding: 1rem 1.5rem;
  border: 1px solid #000;
  font-size: 15px;
  font-weight: bold;
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
  text-align: center;
}

.botones {
  margin-top: 10px;
  
  width: 200px;
  background-color: #18191f;
  color: #fff;
  border: none;
  height: 50px;
  border-radius: 16px;
  font-size: 20px;
  font-weight: 800;
}

.botones #verGastos{
  margin-bottom: 10px;
}

#botones:hover {
  background-color: #434343;
  border: 1px solid black;
  cursor: pointer;
}

#botones:active,
#botones:focus {
  outline: none;
}

#enunciado {
  font-size: 1.2rem;
  font-weight: bold;
  margin: 10px 0 20px 0;
}
#mostrar-ingresos {
  margin-top: 15px;
  width: 350px;
  height: 100px;
  background-color: white;
  border-radius: 16px;
  border: 2px solid black;
  text-align: center;
  text-justify: auto;
}

#img-egresos{
  width: 500px;
  height: 500px;
}



#container {
  width: 450px;
  height: 500px;
  background-color: #D5DBDB;
  border-radius: 16px;
  border: 2px solid white;
  text-align: center;
  font-family: "Ubuntu", sans-serif;
  display: flex;
  justify-content: center;
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
  font-size: 20px;
  background-image: url(../assets/save_money.svg);
}
div img {
  width: 150px;
  height: 150px;
}

.hide {
  display: none;
}
li,
ul {
  width: 100%;
  margin-top: 30px;
  padding: 0;
  list-style: none;
  text-align: center;
}
li p{
  font-size: 20px;
  font-weight: bold;

}
#total{
  font-size: 40px;
  color: crimson;
  font-weight: bold;
  margin-top: 0;
}
#total-titulo{
  font-size: 40px;
  color: black;
  font-weight: bold;
  margin-bottom: 0;
}
</style>