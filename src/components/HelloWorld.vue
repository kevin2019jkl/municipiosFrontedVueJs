<template>
  <v-container grid-list-md>
    <h1>municipios y departamentos</h1>
    <v-layout row wrap>
      <v-flex xs6>
        <v-select
          :items="departamentos"
          item-text="name"
          item-value="id"
          v-model="departamento"
          label="Standard"
          @change="getMuni()"
        ></v-select>
        </v-flex>
        <v-flex xs6>
        <v-select
          :items="municipios"
          item-text="name"
          item-value="id"
          label="Standard"
        ></v-select>
      </v-flex>
    </v-layout>
    
  </v-container>
</template>

<script>
import axios from 'axios'


 const api = axios.create({
    baseURL: 'http://127.0.0.1:8000/api',
    withCredentials: false,
    headers: {
     'Access-Control-Allow-Origin': '*',
     'Accept':'aplication/json',
      'Content-Type':'aplication/json',
      }
   });

export default {
  data(){
    return{
      departamento:0,
      departamentos:[],
      municipios:[]
    }
},
  methods:{

    getMuni(){
      //alert(this.departamento)
      this.municipios=[];
      api.get('/municipios/'+this.departamento).then(response=>{
        this.municipios=response.data;
      }).catch(error=>{
       
      })
    },

    getInit(){
      this.departamentos=[];
      api.get('/departamento').then(response=>{
        this.departamentos=response.data;
      }).catch(error=>{
       
      })
    }
  },
  mounted(){
    this.getInit();
  }
}
</script>
