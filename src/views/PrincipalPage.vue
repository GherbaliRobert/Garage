<template>
    <div class="indexPage">
      <div class="navTop">
        <img class="mecanziareImg" src="../assets/Mecanizare.png" alt="">
        <select name="Auto" id="autoSrch" v-model="typeFilter">
          <option value="0">Selecteaza utilajul</option>
          <option value="1">Platforma</option>
          <option value="2">Abroll</option>
          <option value="3">Perii mari</option>
          <option value="4">Perii medi</option>
          <option value="5">Perii mici</option>
        </select>
        <select name="status" id="status" v-model="statusFilter">
          <option value="0">Toate</option>
          <option value="1">Functionala</option>
          <option value="2">Defect</option>
        </select>
        <input class="inputSrch" type="text" placeholder="Cauta utilaj" v-model="searchFilter">
      </div>
      <div class="content">
        <h2>Listă de Mașini</h2>
        <div id="auto">
          <div v-for="masina in filteredCars" :key="masina.numar_auto" class="carsDivs">
            <p>Tip auto: {{ masina.tip_auto }}</p>
            <p>Număr auto: {{ masina.numar_auto }}</p>
            <p>Stare: {{ masina.stare }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        masini: [],
        typeFilter: "0", 
        statusFilter: "0", 
        searchFilter: "" 
      };
    },
    computed: {
      filteredCars() {
        return this.masini.filter(masina => {
          const tipFiltru = this.typeFilter === "0" || masina.tip_auto === this.typeFilter;
          const stareFiltru = this.statusFilter === "0" || masina.stare === this.statusFilter;
          const cautareFiltru = this.searchFilter === "" || masina.tip_auto.toLowerCase().includes(this.searchFilter.toLowerCase()) || masina.numar_auto.toLowerCase().includes(this.searchFilter.toLowerCase());
          return tipFiltru && stareFiltru && cautareFiltru;
        });
      }
    },
    mounted() {
      this.incarcaDate();
    },
    methods: {
      incarcaDate() {
        fetch("/data/auto.json")
          .then(response => response.json())
          .then(data => {
            this.masini = data;
          });
      }
    }
  };
  </script>
  
  <style>
  html,
  body {
    height: 100%;
    display: block !important;
  }
  #app {
    margin: 1%;
    display: flex;
    justify-content: center;
  }
  .mecanziareImg {
    height: 90%;
  }
  .content {
    display: flex;
    width: 95%;
    flex-direction: column;
  }
  .carsDivs {
    display: flex;
    width: 100%;
    background: crimson;
    margin-bottom: 20px;
    justify-content: space-evenly;
    border-radius: 7px;
  }
  #auto {
    width: 100%;
  }
  .navTop {
    width: 97%;
    height: 100px;
    background: rgb(132, 132, 132);
    display: flex;
    align-items: center;
    border-radius: 0 0 7px 7px;
    justify-content: space-around;
  }
  select {
    width: 200px;
    height: 40px;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 5px;
    font-size: 16px;
    color: #333;
    background-color: #fff;
  }
  .inputSrch {
    width: 250px;
    height: 50px;
  }
  .indexPage {
    border-radius: 7px;
    width: 95%;
    height: 800px;
    background: whitesmoke;
    color: black;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  </style>