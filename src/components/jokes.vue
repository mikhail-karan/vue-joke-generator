<template>
  <div id="jokes">
    <h1>Press a button, get a joke!</h1>
    <div class="joke-container">
      <div v-html="jokeText"></div>
    </div>
    <div v-on:click="generateJoke" class="button">Press me for a laugh</div>
  </div>
</template>

<script>
export default {
  name: 'Jokes',
  data() {
    return {
      jokes: [
        {
          joke: "My wife handed me two kayak paddles and asked, 'Which one do you want?'",
          punchline: "I said I'd take either/oar."
        },
        {
          joke: "Courtesy of my 6yo daughter: What do you call a dinosaur that takes care of its teeth?",
          punchline: "A Flossiraptor"
        },
        {
          joke: "I am a programmer. A journalist asked me what makes a software code bad. I said...",
          punchline: "No comment"
        }
      ],
      joke: "",
      jokeIterator: 0,
      jokeText: ""
    }
  },
  methods: {
    generateJoke: function (){
      let jokeNum = this.jokes.length
      let jokeQuestion = this.jokes[this.jokeIterator].joke;
      let jokePunchline = this.jokes[this.jokeIterator].punchline;
      this.jokeText = jokeQuestion + "<br>" + jokePunchline;
      if (this.jokeIterator < jokeNum-1){ this.jokeIterator++} else {this.jokeIterator = 0}
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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

#jokes {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.joke-container {
  height: 10vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin: 10px 0;
  flex-direction: column;
}

.button {
  user-select: none;
  padding: 10px;
  color: #fff;
  background-color: #42b983;
  width: 20vw;
}
</style>
