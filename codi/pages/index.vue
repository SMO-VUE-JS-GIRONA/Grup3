<template>
  <v-container>
    <v-row class="contenidor">
      <v-col cols="6">
        <div v-if="search">
          <v-card class="persones"  v-for="persona in personesFiltrades" :key="persona.nom">
            <v-card-text >
              <h2>{{persona.nom}}</h2><br>
              <h3>{{persona.edat}}</h3>
            </v-card-text>
          </v-card>
        </div>
        <div v-else-if="nomBorrar">
          <v-card class="persones" v-for="persona in persones" :key="persona.nom">
            <v-card-text>
              <h2>{{persona.nom}}</h2><br>
              <h3>{{persona.edat}}</h3>
            </v-card-text>
          </v-card>
        </div>
        <div v-else>
          <v-card class="persones" v-for="persona in personesFiltradesEdat" :key="persona.nom">
            <v-card-text>
              <h2>{{persona.nom}}</h2><br>
              <h3>{{persona.edat}}</h3>
            </v-card-text>
          </v-card>
        </div>
      </v-col>
      <v-col cols="6">
        <v-btn @click="ordenarAZ()">ORDENAR AZ (1)</v-btn><br><br>
        <v-btn @click="trobarGran()">TROBAR MÉS GRAN (2)</v-btn>
        <v-text-field v-model="search" label="Cercar Persones (3)" @input="filtrarPersones()"></v-text-field>
        <v-text-field v-model="nomBorrar" label="Nom Persona per Borrar (4)"></v-text-field>
        <v-btn @click="borrar(nomBorrar)">BORRAR (4)</v-btn><br><br>
        <v-btn @click="ordenarLength()">ORDENAR LENGTH (5)</v-btn>
        <v-text-field v-model="searchEdat" label="Cercar Persona per Edat (6)" @input="filtrarPersonesEdat()"></v-text-field>
        <h1 style="font-size:16px; color: blue;">Exercici 12 Gener - Grup 3 (Hicham Oukassou, Helena Artola i Gonzalo Molina)</h1>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
// 1. Ordenar un array de persones alfabèticament segons el seu nom. (OK)

// 2. Trobar i escriure a la consola la persona amb l'edat més gran (OK)

// 3. Trobar la persona amb un cert nom en un array de persones (OK)

// 4. Eliminar la persona amb un cert nom en un array de persones

// 5. Ordenar un array javascript de persones segons el tamany del nom de la persona (OK)

// 3. Trobar la persona amb una certa edat en un array de persones (OK)

export default {
  data() {
    return {
      persones: [
        {
          nom:"Eva",
        edat:"26"
    },
    {
        nom:"Pep",
        edat:"21"
      },
      {
        nom:"Jordi",
        edat:"31"
    },
    {
        nom:"Angèlica",
        edat:"25"
      },
    {
        nom:"Mar",
        edat:"52"
      },
      {
        nom:"David",
        edat:"78"
      },
    ],

    personaGran: [],
    search:'',
    personesFiltrades:[],
    personesFiltradesEdat: [],
    searchEdat:'',
    nomBorrar: '',
  }
},
methods: {
  ordenarAZ() {
    this.persones.sort(function(a,b) {
      if (a.nom > b.nom) {
        return 1;
      }
      if (a.nom < b.nom) {
        return -1;
      }
        return 0;
      })
      console.log(this.persones)
    },
    trobarGran() {
      let maxim = -Infinity;
      this.persones.forEach((el, index, array) => {
        if (this.persones[index].edat > maxim) {
          maxim = this.persones[index].edat;
          this.personaGran = this.persones[index].nom;
        }
      })
      console.log(`La persona amb l'edat més gran és: ${this.personaGran} i té ${maxim} anys.`);
    },
    filtrarPersones(search) {
      this.personesFiltrades = this.persones.filter(persona => persona.nom.toLowerCase().includes(this.search.toLowerCase()));
      console.log(search);
    },
    ordenarLength() {
      this.persones.sort(function(a,b) {
        if (a.nom.length > b.nom.length) {
          return 1;
        }
        if (a.nom.length < b.nom.length) {
          return -1;
        }
          return 0;
        })
        console.log(this.persones)
      },
      filtrarPersonesEdat(searchEdat) {
      this.personesFiltradesEdat = this.persones.filter(persona => persona.edat.toLowerCase().includes(this.searchEdat.toLowerCase()));
      console.log(searchEdat);
    },
    borrar(nomBorrar) {
      this.persones = this.persones.filter(persona => persona.nom !== nomBorrar);
      this.personesFiltrades = this.personesFiltrades.filter(persona => persona.nom !== nomBorrar);
      this.personesFiltradesEdat = this.personesFiltradesEdat.filter(persona => persona.nom !== nomBorrar);
      this.nomBorrar ='';
    },
  },
  created() {

    this.personesFiltrades = this.persones
    this.personesFiltradesEdat = this.persones
  },
}
</script>

<style scoped>
.contenidor {
  border: solid 1px black;
}

.persones{
  background-color:aquamarine;
  margin:10px;
  color:black;
  border-radius: 10%;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  font-size: 10px;
  
}
</style>