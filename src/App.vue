<template>
  <div id="app">
    <blockquote v-on:click="displayQuote()">
      <p>{{currentQuote.content}}</p>
      <footer>
      — <cite>{{currentQuote.author}}</cite>
      <p>Your user agent: {{userAgent}}</p>
      </footer>
    </blockquote>
  </div>
</template>


<script>
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
       userAgent: '',
      currentQuote: {},
      quotes: [
        {
          content: "Overcoming fear and conceiving this 'art of more' should be a fundamental practice in what it is that you do and make.",
          author: "Chase Jarvis"
        },
        {
          content: "As everything in this world is but a sham, Death is the only sincerity",
          author: "Yamamoto Tsunetomo"
        },
        {
          content: "The world needs actual excitement and emotion more than it needs cool people.",
          author: "Amanda Palmer"
        }
      ]
    }
  },
  created: function() {
    this.displayQuote();
  },
  methods: {
    displayQuote: function(){
      var self = this;
      var randomInt = Math.floor(Math.random() * (this.quotes.length - 0));
      this.currentQuote = this.quotes[randomInt];

      axios.get('http://httpbin.org/user-agent')
      .then(response => {
        self.userAgent = response.data['user-agent'];
      })
      .catch(error => {
        console.log(error);
      })
  }
  }
}
</script>

<style lang="scss">
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
