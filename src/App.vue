<template>
  <div id="app" class="container">
    
    <!-- //////////////////////////////formularion de creación de pregunta////////////////////////////////////////--> 
    <div class="row-fluid">
      <form id="form">
        <div class="form-group">
          <label for="contentId">Pregunta</label>
          <input type="text" class="form-control" id="contentId" aria-describedby="contentHelp" v-model="question.text">
        </div>
        <button type="submit" class="btn btn-primary" @click.prevent="create">Crear</button>
      </form>
      <hr />
      
      <p v-if="loading">Loading ...</p>
      <div class="row-fluid" v-else>
        <div class="card bg-light text-dark" v-for="item in questions" :key="question._id">
          <div class="card-body">
              <h5 class="card-title">{{item.text}}</h5> 
              <div  v-for="answer in item.answers">
                <label>Responder</label>
                <input type="text" class="form-control"  v-model="answer.text">
                <button type="submit" class="btn btn-primary" @click.prevent="create">Crear</button>
              </div>
              
              
          </div>
        </div>
      </div>
    </div>
    
    <!-- ////////////////////////////fin de formulario de creacion de pregunta ////////////////////////////////-->
   
    
    
  </div>
</template>

<script>
import axios from "axios";
import config from "./config.json";

export default {
  name: 'app',
  data () {
    return {
      loading: true,
      questions: [],
      question: {
        text: '',
        answers:[]
      }
    }
  },
  
  
  created (){
    this._loadQuestions();
    this._loadAuthors();
  },
  methods: {
    _loadQuestions(){
      console.log('--------cargando los questions---------')
      axios.get(`${config.baseURL}/questions`,{
        withCredentials: true
      })
      .then( response => {
        this.loading = false;
        this.questions = response.data.data;
      })
    },
    _loadAuthors(){
      axios.get(`${config.baseURL}/users`,{
        withCredentials: true
      })
      .then( response => {
        this.authors = response.data.data;
      })
    },
    create(){
      
      let payload = "";
      Object.keys(this.tweet).forEach(key => {
        payload+=`${key}=${this.tweet[key]}&`
      });
      
      axios.post(`${config.baseURL}/questions`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        document.getElementById("form").reset();
        this._loadQuestions();
      })
    }
  }
}
</script>