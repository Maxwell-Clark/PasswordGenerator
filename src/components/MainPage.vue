<template>
  <div id="main">
      <h1 class="title">Password Generator 3000</h1>
      <div class="body" id="password">{{password}}</div>
      <div v-if="message != null" class="message">{{message}}</div>
      <button class="button" @click="this.generatePassword">New Password</button>
      <input min="3" max="30" class="input" type="number" placeholder="Password Length" v-model="passwordLength">
      <button 
        v-clipboard:copy="password"
        v-clipboard:success="onCopy"
        v-clipboard:error="onError"
        class="button">Copy Password</button>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            password: [],
            passwordLength: 8,
            message: null
        }
    }, 
    methods: {
        generatePassword() {
            this.message = null
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz123456789+*#$*/=%^[]~&|'
            this.password = []
            for(let i = 0; i < this.passwordLength; i++) {
                this.password.push(characters.charAt(Math.floor(Math.random() * characters.length)))
            }
            this.password = this.password.join('')
        },
        onError() {
            this.message = 'there was an error'
        },
        onCopy() {
            this.message = 'Password Copied'
        }
    },
    mounted() {
        this.generatePassword()
    }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Zen+Dots&display=swap');
    #main {
        background-color: #2b5329;
        border: 2px solid black;
        border-radius: 6px;
        padding: 1em;
        width: 60%;
        margin: 0px !important;
    }
    html {
        overflow: scroll;
    }
    ::-webkit-scrollbar {
        width: 1px;
        background: transparent; /* make scrollbar transparent */
    }
    .title {
        background-color: #2b5329;
        color: black;
        font-family: 'Zen Dots', sans-serif;
        border: 1px solid transparent;
        border-radius: 6px;
    }
    .body {
        margin-top: 1em;
        padding: 2em;
        font-size: large;
        color: #149414;
        font-family: 'Zen Dots', sans-serif;
        border: 2px solid #8D99AE;
        background-color: black;
        border-radius: 6px;
        overflow-x: scroll;
    }
    .message {
        background-color: #649568;
        color: #9ccc9c;
        font-family: 'Zen Dots', sans-serif;
        margin-top: 1em;
        padding: 1em;
        border: 1px solid;
        border-radius: 1em;
    }
    .button {
        margin-top: 1em;
        background-color: black;
        border: 2px solid #8D99AE;
        font-family: 'Zen Dots', sans-serif;
        color: #149414;
        border-radius: 1em;
        height: 4em;
    }
    .input {
        margin: 1em;
        border: 2px solid #8D99AE;
        font-family: 'Zen Dots', sans-serif;
        border-radius: 1em;
        color: #149414;
        height: 3.5em;
        width: 5em;
        text-align: center;
        background-color: black;
    }
    
</style>