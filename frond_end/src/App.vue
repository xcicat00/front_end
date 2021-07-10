<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h6>Made by Láďa Čičátko</h6>
    <h6> </h6>
    <table class="table">
  <thead class="thead-light">
    <tr>
      <th scope="col">_id</th>
      <th scope="col">Jméno</th>
      <th scope="col">Příjmeni</th>
      <th scope="col">Email</th>
      <th scope="col">Telefon</th>
      <th scope="col">Ulice</th>
      <th scope="col">Město</th>
      <th scope="col">PSČ</th>

    </tr>
  </thead>
  <tbody>
    <tr v-for="kontakt in this.kontakty">
      <td>{{ kontakt._id }}</td>
      <td>{{ kontakt.Jmeno }}</td>
      <td>{{ kontakt.Prijmeni }}</td>
      <td>{{ kontakt.Email }}</td>
      <td>{{ kontakt.Tel }}</td>
      <td>{{ kontakt.Ulice }}</td>
      <td>{{ kontakt.Mesto }}</td>
      <td>{{ kontakt.PSC }}</td>
      <td><button type="button" class="btn btn-danger" href='"http://localhost:8080/list_user/" + kontakt.Prijmeni'>Delete</button></td>
      <td><button types="button" class="btn btn-primary" data-toggle="modal"
                            data-target="#editBookModal" onClick="setEditModal(${book.isbn})">
                            Edit
                            </button></td>

    </tr>
  </tbody>
</table>
    <h2>Essential Links</h2>

    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs hovno hovno hovno</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
const axios = require('axios');

export default {
  name: 'app',
  data () {
    return {
      msg: 'Vítejte v adresáři',
      kontakty:[]
    }
  },
  methods:{vycti_kontakty(){
    axios
                    .get(`http://localhost:8080/list_user`)
                    .then(response => {
                        console.log(response.data);
                        this.kontakty = response.data;
                    });
    }
  },
  mounted() {
        this.vycti_kontakty();
    },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
