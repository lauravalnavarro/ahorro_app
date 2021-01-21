<template>
  <div id="app">
    <div class="header">
      <h1>Finanzas Sanas</h1>
      <nav>
        <button @click="init">Ingresos</button>
        <button @click="egresos">Egresos</button>
      </nav>
    </div>

    <div class="main-component">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data: function () {
    return {};
  },
  computed:{

  },
  methods: {
    init: function () {
      this.$router.push({ name: "user" });
    },
    ingresos: function () {
      this.$router.push({ name: "user_balance" });
    },
    egresos: function() {
      this.$router.push({ name: "user_egresos" })
    }
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:ital,wght@1,300&display=swap");
body {
  margin: 0 0 0 0;
}
.header {
  margin: 0%;
  padding: 0;
  width: 100%;
  height: 20px;
  min-height: 70px;
  color: #e5e7e9;
  font-family: 'Roboto', sans-serif;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(48,48,48, 0.8 ); /* fallback for old browsers */
  
}
.header h1 {
  width: 20%;
  text-align: center;
  margin: 5%;
  font-family: 'Roboto', sans-serif;
  cursor: pointer;
}
.header nav {
  height: 100%;
  width: 45%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
}
.header nav button {
  margin: 15px;
  color: #e5e7e9;
  background: #283747;
  border: 1px solid #e5e7e9;
  border-radius: 5px;
  padding: 10px 20px;
}
.header nav button:hover {
  color: #283747;
  background: #e5e7e9;
  border: 1px solid #e5e7e9;
}


.main-component {
  height: 92vh;
  margin: 0%;
  padding: 0%;
  background: #fdfefe;
}
.footer {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 10vh;
  min-height: 100px;
  background-color: #283747;
  color: #e5e7e9;
}
.footer h2 {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
