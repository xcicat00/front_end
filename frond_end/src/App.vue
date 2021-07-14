<template>
<div id="app">
  <div>
    <h1>{{ msg }}</h1>
    <h6  color="blue" >Made by Láďa Čičátko</h6>
    <button type="button" class="btn btn-primary" data-toggle="button">
    Zadej kontakt
    </button>
  </div>  
<div v-shov="ukazZadejKontakt">  
<form>  
  <label class="h2" align="left">Nový kontakt </label>
    <div class="form-row">
      <div class="form-group col-md-3">
    
        <input type="text" class="form-control" placeholder="Jméno">
      </div>
      <div class="form-group col-md-3">
        <input type="text" class="form-control" placeholder="Příjmení">
      </div>
    </div>
    <div class="form-row">
      <div class="form-group col-md-4">
        <input type="email" class="form-control" id="inputEmail4" placeholder="Email">
      </div>
      <div class="form-group col-md-2">
        <input type="text" class="form-control" id="inputTel" placeholder="Tel">
      </div>
    </div>
    <div class="form-group col-md-6">
      <input type="text" class="form-control" id="inputAddress" placeholder="Ulice">
    </div>
    <div class="form-row">
      <div class="form-group col-md-4">
        <input type="text" class="form-control" id="inputCity" placeholder="Město">
      </div>
    
      <div class="form-group col-md-2">
        <input type="text" class="form-control" id="inputZip" placeholder="PSČ">
      </div>
    </div>
  
    <div class="form-group col-md-6">
      <button type="submit" class="btn btn-primary">Vlož kontakt</button>
    </div>
</form>
</div>

<div>
    <label class="h2">Kontakty</label>
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
      <td><button type="button" class="btn btn-danger" id=kontakt._id  onClick="smazKontakt(${kontakt.Jmeno})">Delete</button></td>
      <td><button types="button" class="btn btn-primary" data-toggle="modal"
                            data-target="#editBookModal" onClick="setEditModal(${book.isbn})">
                            Edit
                            </button></td>

    </tr>
  </tbody>
  </table>
  </div>
</div>
</template>

<script>
const axios = require('axios');

export default {
  name: 'app',
  data () {
    return {
      msg: 'Vítejte v adresáři',
      kontakty:[],
      ukazZadejKontakt: false
    }
  },
  methods:{vycti_kontakty(){
    axios
                    .get(`http://localhost:8080/list_user`)
                    .then(response => {
                        console.log(response.data);
                        this.kontakty = response.data;
                    });
    },
    zapis_kontakt(){
      axios
            .post(`http://localhost:8080/vloz_user.html`)
    },
    smazKontakt(jmeno){
      console.log(jmeno);
    },
    toggleUkazKontakt(){
      console.log('toggle');
      this.ukazZadejKontakt = !this.ukazZadejKontakt;
      console.log("Boolean: " + this.ukazZadejKontakt);
    }
  },

  mounted() {
        this.vycti_kontakty();
        this.zapis_kontakt();
        this.smazKontakt();
        this.toggleUkazKontakt();
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

h6 {
  color: green;
  font-weight: bold;
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
