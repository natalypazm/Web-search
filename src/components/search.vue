<template>
  <div class="body-search">
    <div class="div-search">
      <h2>Busca tus canciones, películas favoritas y más!</h2>
      <p>Ingresa tu búsqueda y te mostraremos las incidencias que encontremos en nuestra API.</p>
      <input type="text" class="input-search" v-model="query" placeholder="Ej. Maluma">
      <button class="button-search" @click="search">Buscar</button>
    </div>
    <div class="table-list grid-item"> 
        <div class="item" v-for="data in list" :key='data.id'>
          <span v-if="data.source==='apple'">
            <img width="30px" src="../assets/apple.png" alt="apple">
          </span>
          <span v-if="data.source==='tvmaze'">
            <img width="30px" src="../assets/tvmaze.png" alt="tvmaze">
          </span>
          <span> {{data.source}} - {{data.name}} - {{data.type}}</span>
        </div>
    </div>
  </div>
</template>

<script>
var backend = 'http://localhost:4300/search';
const axios = require('axios');
export default {
  name: 'Search',
  data(){
  return{
    query: '',
    resultNone: false,
    list: []
  }
  },
  methods: {
    search: function () {
        axios.get(backend + '?q=' + this.query).then(response => {
            this.list = response.data.data;
        });
    },
  },
}
</script>


<style scoped>
  *{font-family: 'PT Sans', sans-serif;}
  body{
    font-family: 'PT Sans', sans-serif;
    height:100vh;
    padding:10px;
  }
  input[type="text"],button,span{font-family: 'PT Sans', sans-serif;}
  .body-search{
    display: flex;
    justify-content: space-evenly;
  }
  .div-search{
    width: 40%;
    align-items: center;
    margin: auto 0;
  }
  .input-search{
    padding:10px;
    width:300px;
    border:1px solid #ccc;
  }
  .table-list{
    width:40%;
    box-shadow: 0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12);
    height:90vh;
    overflow:auto;
    margin:20px 0;
  }
  .item{border-bottom:1px solid #ddd;padding:1rem;}
  .button-search{margin-left:1rem;cursor:pointer;background: #3949ab;border: none;border-radius:25px;opacity: 0.8;transition:all .25s;color: #fff;padding: 5px 50px;font-size: 20px;}
  .button-search:hover{transform:scale(0.965);opacity:1;transition:all .25s;}
</style>
