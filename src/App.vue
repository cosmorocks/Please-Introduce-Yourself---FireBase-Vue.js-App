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

      <div class="card-columns">
        <div class="card" v-for="message in messages">
          <div class="card-block">
            <h5 class="card-title"> {{message.title}} </h5>
            <p class="card-text"> {{ message.text }} </p>
            <p class="card-text"><small class="text-muted"> Added on {{ dateToString(message.timestamp) }} </small> </p>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
  import Firebase from 'firebase'
  import { dateToString } from './utils/utils'
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
    }
  }
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
