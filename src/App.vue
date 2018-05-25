<template>
  <div id="app" class="jumbotron">
    <div class = "container">
      <h1>Hello! Nice to meet you! </h1>
      <hr />
      
      <form @submit="addMessage">
        <div class="form-group">
          <input class="form-control" v-model="newMessage.title" maxlength="40" autofocus placeholder="Please introduce yourself :)"/>
        </div>
        <div class="form-group">
          <textarea class="form-control" v-model="newMessage.text" placeholder="Leave your message!" rows="3">
          </textarea>
        </div>
        <button class="btn btn-primary" type="submit">Send</button>
      </form>

      <hr/>
  
      <template>
        <div class="card-columns">
          <card class="border-success">
            <data v-bind:title="'Hello!'" v-bind:text="'This is our fixed card!'" v-bind:footer="'Added on ' + dateToString(Date.now())">
            </data>
          </card>
        </div>
      </template>
      <!-- ////////// -->
      <!--
      <div class = "card-columns">
        <card v-for="message in messages" v-bind:title="message.title" v-bind:text="message.text" v-bind:footer="'Added on ' + dateToString(message.timestamp)">
          <data v-bind:title="message.title"></data>
        </card>
      </div> -->
      </div> 

    </div>
</template>

<script>
  import Firebase from 'firebase'
  import { reverse } from './utils/utils'
  import { dateToString } from './utils/utils'
  import Card from './components/Card'
  import Data from './components/Data'

  // Initialize Firebase
  let config = {
    apiKey: "AIzaSyAUwhsDODsFsc5Oi694aqihlBFCTUoASXI",
    authDomain: "pleaseintroduceyoself.firebaseapp.com",
    databaseURL: "https://pleaseintroduceyoself.firebaseio.com",
    projectId: "pleaseintroduceyoself",
    storageBucket: "pleaseintroduceyoself.appspot.com",
    messagingSenderId: "149184767267"
  }
  let app = Firebase.initializeApp(config);
  
  let db = app.database()
  let messagesRef = db.ref('messages')

  export default {
    name: 'App',
    firebase:{
      messages: messagesRef
    },
    data () {
      return {
        newMessage: {
          title:'',
          text:'',
          timestamp:null
        }
      }
    },
    methods: {
      addMessage(e){
        if(this.newMessage.title === ''){
          return
        }
        e.preventDefault()
        this.newMessage.timestamp = Date.now()
        messagesRef.push(this.newMessage)
        this.newMessage.text = ''
        this.newMessage.title = ''
        this.newMessage.timestamp = null
      },
      dateToString
    },
    components: {
      Card,
      Data
    }
  }
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
