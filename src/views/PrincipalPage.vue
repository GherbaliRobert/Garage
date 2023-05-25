<template>
    <div class="indexPage">
      <div class="navTop">
        <img class="mecanziareImg" src="../assets/Mecanizare.png" alt="">
        <select name="Auto" id="autoSrch" @change="onChange($event, 'auto')" v-model="test">
          <option value="Default">Selecteaza utilajul</option>
          <option value="Platforma">Platforma</option>
          <option value="Abroll">Abroll</option>
          <option value="Camion">Camion</option>
          <option value="SUV">SUV</option>
        </select>
        <select name="status" id="status" @change="onChange($event, 'status')">
          <option value="Default">Toate</option>
          <option value="Functionala">Functionala</option>
          <option value="Defect">Defect</option>
        </select>
        <input class="inputSrch" type="text" placeholder="Cauta utilaj" @input="onChange($event, 'search')">
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
        typeFilter: "Default", 
        statusFilter: "Default", 
        searchFilter: "",
        filteredCars: [],
        test: 'Default'
      };
    },
    mounted() {
      this.incarcaDate();
    },
    watch: {
      'test' () {
        console.log('test')
      }
    },
    methods: {
      onChange(event, type) {
        const value = event.target.value;
        switch(type) {
          case 'auto':
            this.typeFilter = value;
            if(this.statusFilter === 'Default') {
              if(value !== 'Default') {
                this.filteredCars = this.masini.filter(m => m.tip_auto === value);
              } else {
                this.filteredCars = this.masini;
              }
            } else {
              if(value !== 'Default') {
                this.filteredCars = this.masini.filter(m => m.tip_auto === value && m.stare === this.statusFilter);
              } else {
                this.filteredCars = this.masini.filter(m => m.stare === this.statusFilter);
              }
            }
            break;
          case 'status':
            this.statusFilter = value;
            if(this.typeFilter === 'Default') {
              if(value !== 'Default') {
                this.filteredCars = this.masini.filter(m => m.stare === value);
              } else {
                this.filteredCars = this.masini;
              }
            } else {
              if(value !== 'Default') {
                this.filteredCars = this.masini.filter(m => m.stare === value && m.tip_auto === this.typeFilter);
              } else {
                this.filteredCars = this.masini.filter(m => m.tip_auto === this.typeFilter);
              }
            }
            break;
          case 'search':
            if(value !== '') {
              this.filteredCars = this.filteredCars.filter(c => c.stare.includes(value) || c.numar_auto.includes(value) || c.tip_auto.includes(value))
            } else {
              this.filteredCars = this.masini;
            }
            break;
          default:
            break;
        }
      },
      incarcaDate() {
        fetch("/data/auto.json")
          .then(response => response.json())
          .then(data => {
            this.masini = data;
            this.filteredCars = data;
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