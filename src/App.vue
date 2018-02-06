<template>
  <div id="app">
    
    <br>
    
    <b-container class="bv-example-row">
        <b-row>
            
            <b-col cols="12" md="12" v-if="!logged">
              <!-- Using modifiers -->
              <b-btn v-b-modal.signUp>Sign Up</b-btn>
              <b-btn v-b-modal.signIn>Sign In</b-btn>
            </b-col>
            
            <b-col cols="12" md="12" v-else>
                <i>Welcome </i> <a href="#">{{ user.firstname }} {{ user.lastname }}</a>
                <b-button @click.prevent="signout" variant="secondary" class="float-right">Sign Out</b-button>
            </b-col>
              <hr />
        </b-row>
    </b-container>

    <!-- the modal signUp-->
    <b-modal id="signUp" ref="signUp" hide-footer>
     <b-container class="bv-example-row">
        <b-row>
             <b-col cols="12" md="12">
              <h1>Sign Up</h1>
               <b-form id="signup">
                <b-form-group id="grupo1"
                              label="firtname:"
                              label-for="firstname">
                  <b-form-input name="firstname"
                                type="text"
                                v-model="user.firstname"
                                required
                                placeholder="Escribe tu firtname">
                  </b-form-input>
                </b-form-group>
                
       
                <b-form-group id="grupo2"
                              label="lastname:"
                              label-for="lastname">
                  <b-form-input name="lastname"
                                type="text"
                                v-model="user.lastname"
                                required
                                placeholder="Escribe tu lastname">
                  </b-form-input>
                </b-form-group>
                
                <b-form-group id="grupo3"
                              label="email:"
                              label-for="email">
                  <b-form-input name="email"
                                type="email"
                                v-model="user.email"
                                required
                                placeholder="Escribe tu email">
                  </b-form-input>
                </b-form-group>
                
                <b-form-group id="grupo4"
                              label="password:"
                              label-for="password">
                  <b-form-input name="password"
                                type="password"
                                v-model="user.password"
                                required
                                placeholder="Escribe tu password">
                  </b-form-input>
                </b-form-group>
                
                <div slot="modal-footer" class="w-100">
                  <b-button @click.prevent="signup" variant="primary" class="float-right">Create</b-button>
                  <b-button type="reset" variant="danger" class="float-right">Reset</b-button>
               </div>


              </b-form>
               
             </b-col>
        </b-row>
    </b-container>
    </b-modal>
     
    <!-- the modal Login-->
    <b-modal id="signIn" ref="signIp" hide-footer>
     <b-container class="bv-example-row">
        <b-row>
             <b-col cols="12" md="12">
              <h1>Sign In</h1>
               <b-form id="signin">

                <b-form-group id="grupo5"
                              label="email:"
                              label-for="email">
                  <b-form-input name="email"
                                type="email"
                                v-model="userLogin.email"
                                required
                                placeholder="Escribe tu email">
                  </b-form-input>
                </b-form-group>
                
                <b-form-group id="grupo6"
                              label="password:"
                              label-for="password">
                  <b-form-input name="password"
                                type="password"
                                v-model="userLogin.password"
                                required
                                placeholder="Escribe tu password">
                  </b-form-input>
                </b-form-group>
                
                <div slot="modal-footer" class="w-100">
                  <b-button @click.prevent="signin" variant="primary" class="float-right">Login</b-button>
                  <b-button type="reset" variant="danger" class="float-right">Reset</b-button>
               </div>


              </b-form>
               
             </b-col>
        </b-row>
    </b-container>
    </b-modal>
    
    
    <!-- the modal CreateAnswer-->
    <b-modal id="createAnswerModal" hide-footer>
     <b-container class="bv-example-row">
        <b-row>
             <b-col cols="12" md="12">
              <h1>Create answer</h1>
               <b-form id="createAnswerForm">

                <b-form-textarea name="text"
                     v-model="answer.text"
                     placeholder="Enter answer"
                     :rows="3"
                     :max-rows="6">
                </b-form-textarea>
                
                <br>
                <div slot="modal-footer" class="w-100">
                  <b-button @click.prevent="createAnswer" variant="primary" class="float-right">Create</b-button>
                  <b-button type="reset" variant="danger" class="float-right">Reset</b-button>
               </div>


              </b-form>
               
             </b-col>
        </b-row>
    </b-container>
    </b-modal>
    
    
    <b-modal id="editQuestionModal" hide-footer>
     <b-container class="bv-example-row">
        <b-row>
             <b-col cols="12" md="12">
              <h1>Edit Question</h1>
               <b-form id="editQuestionForm">

                <b-form-textarea name="text"
                     v-model="answer.text"
                     placeholder="Enter Question"
                     :rows="3"
                     :max-rows="6">
                </b-form-textarea>
                
                <br>
                <div slot="modal-footer" class="w-100">
                  <b-button @click.prevent="editQuestion" variant="primary" class="float-right">Edit</b-button>
                  <b-button type="reset" variant="danger" class="float-right">Reset</b-button>
               </div>


              </b-form>
               
             </b-col>
        </b-row>
    </b-container>
    </b-modal>
    
    
    
    
     <b-container class="bv-example-row">
        <b-row>
             <b-col cols="12" md="12">
               <b-form id="createQuestionForm" v-if="logged">

                <b-form-group id="grupo7"
                              label="Question:"
                              label-for="text">
                  <b-form-input name="text"
                                type="text"
                                v-model="question.text"
                                required
                                placeholder="Escribe tu Question">
                  </b-form-input>
                </b-form-group>
  
                
                
                <b-button @click.prevent="createQuestion" variant="primary" >Create</b-button>
                <b-button type="reset" variant="danger" >Reset</b-button>



              </b-form>
              
              <hr />
              <p v-if="loading">Loading ...</p>
              
              <div v-else>
                <h1>Questions</h1>
                
                <b-list-group>
                  
                  <b-list-group-item class="flex-column align-items-start" v-for="question in questions" :key="question._id">
                    <div class="d-flex w-100 justify-content-between">
                      <b-badge variant="success"><h6 class="mb-1">{{ question.user.firstname }} {{ question.user.lastname }}</h6></b-badge>
                      <small v-bind:id="question._id">
                        {{ moment(question.createdAt, "YYYYMMDD").fromNow() }}
                        <b-btn v-b-modal.createAnswerModal variant="success" size="sm" @click="getQuestionId($event)" v-if="logged">Create answer</b-btn>
                        <b-btn v-b-modal.editQuestionModal variant="primary" size="sm" @click="getQuestionId($event)" v-if="logged">Edit</b-btn>
                        <b-btn variant="danger" size="sm" @click="deleteQuestion($event)" v-if="logged">Delete</b-btn>
                      </small>
                    </div>
                    <p class="mb-1">
                      <blockquote>{{ question.text }}</blockquote>
                    </p>

                    <small>
                      <b-media v-for="(item, index) in question.answer" >
                        <b-img slot="aside" blank blank-color="#bac" width="64" alt="placeholder" />
                          <a href="#"><p class="mt-0"> {{ item.user.firstname }} {{ item.user.lastname }} - ({{ moment(item.createdAt, "YYYYMMDD").fromNow() }}) </p></a>
                          <p class="mb-0">
                           <i>{{ item.text }}</i>
                          </p>
                          <hr>
                        </b-media>
                    </small>
                    
                  </b-list-group-item>
                 
                </b-list-group>
                
                
              </div>
               
             </b-col>
        </b-row>
    </b-container>
    
    
    
    
  </div>
</template>

<script>
import axios from "axios";
import config from "./config.json";
import serialize from 'form-serialize';
import moment from 'moment';

export default {
  name: 'app',
  data () {
    return {
      logged: false,
      loading: true,
      questions: [],
      answers: [],
      userId: '',
      id_question: '',
      user: {
        firstname: '',
        lastname: '',
        email: '',
        password: '',
      },
      question: {
        text: '',
        user: ''
      },
      userLogin: {
        email: '',
        password: ''
      },
      answer:{
        text: '',
        user: ''
      }
    }
  },
  created (){
    this._loadQuestions();
    if(window.localStorage.getItem('token')){
      this.logged = true;
    }
  },
  methods: {
    _loadQuestions(){
      axios.get(`${config.baseURL}/questions`,{
        withCredentials: true
      })
      .then( response => {
        this.loading = false;
        this.questions = response.data.data;
      })
    },
    createQuestion(){
      const form = document.getElementById('createQuestionForm');
      let payload = serialize(form);
      payload+=`&token=${window.localStorage.getItem('token')}`;
      axios.post(`${config.baseURL}/questions`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        this._loadQuestions();
      })
    },
    deleteQuestion(e){
      this.id_question = e.currentTarget.parentElement.id;
      let payload =`&token=${window.localStorage.getItem('token')}`;
      axios.post(`${config.baseURL}/questions/${this.id_question}/delete`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        this._loadQuestions();
      })
    },
    createAnswer(){
      const form = document.getElementById('createAnswerForm');
      let payload = serialize(form);
      payload+=`&token=${window.localStorage.getItem('token')}`;
      axios.post(`${config.baseURL}/answers`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        let payload_answer = "";
        payload_answer+=`&answer=${response.data._id}&token=${window.localStorage.getItem('token')}`;
        axios.post(`${config.baseURL}/questions/${this.id_question}/answer`, payload_answer, {
          withCredentials: true,
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
          }
        })
        .then( response => {
         this._loadQuestions();
        })
        
      })
    },
    editQuestion(){
      const form = document.getElementById('editQuestionForm');
      let payload = serialize(form);
      payload+=`&token=${window.localStorage.getItem('token')}`;
      axios.post(`${config.baseURL}/questions/${this.id_question}`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        this._loadQuestions();
      })
    },
    signup(){
      const form = document.getElementById('signup');
      const payload = serialize(form);
      axios.post(`${config.baseURL}/users/signup`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        this.logged = true;
        this.userId = response.data.data.user;
        window.localStorage.setItem('token', response.data.token);
      })
    },
    signin(){
      const form = document.getElementById('signin');
      const payload = serialize(form);
      axios.post(`${config.baseURL}/users/login`, payload, {
        withCredentials: true,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })
      .then( response => {
        this.logged = true;
        this.userId = response.data.user._id;
        this.user.firstname = response.data.user.firstname;
        this.user.lastname = response.data.user.lastname;
        window.localStorage.setItem('token', response.data.token);
      })
    },
    signout(){
      this.logged = false;
      window.localStorage.removeItem('token');
    },
    moment: function (date) {
      return moment(date);
    },
    getQuestionId: function(e){
      console.log(e.currentTarget.parentElement.id);
      this.id_question = e.currentTarget.parentElement.id;
    },
    isMyQuestion: function(obj){
      console.log(obj);
      /*axios.get(`${config.baseURL}/questions/${e.target.parentElement.id}`,{
        withCredentials: true
      })
      .then( response => {
        if(response.data.data.user == this.userId){
          return true;
        }else{
          return false;
        }
        
      })*/
    }
  }
}
</script>