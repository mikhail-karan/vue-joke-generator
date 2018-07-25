<template>
  <div id="jokes">
    <h1>Press a button, get a joke!</h1>
    <div class="joke-container">
      <div v-html="jokeText"></div>
      <div class="author" v-html="author"></div>
      <div class="link" v-html="link"></div>
    </div>
    <div v-on:click="generateJoke" class="button">Press me for a laugh</div>
  </div>
</template>

<script>
import JQuery from 'jquery';

const $ = JQuery;

export default {
  name: 'Jokes',
  data() {
    return {
      jokes: [],
      joke: '',
      jokeIterator: 1,
      jokeText: '',
      author: '',
      link: '',
    };
  },
  methods: {
    generateJoke() {
      const jokeNum = this.jokes.length;
      const jokeQuestion = this.jokes[this.jokeIterator].joke;
      const jokePunchline = this.jokes[this.jokeIterator].punchline;
      this.jokeText = `${jokeQuestion}<br><br>${jokePunchline}`;
      this.author = `Reddit User: ${this.jokes[this.jokeIterator].author}`;
      this.link = `<a href=http://reddit.com${this.jokes[this.jokeIterator].link}>Source</a>`;
      if (this.jokeIterator < jokeNum - 1) { this.jokeIterator = this.jokeIterator + 1; } else { this.jokeIterator = 1; } // make sure iterator is always in scope
    },
  },
  created() {
    const _this = this;
    const _jokes = this.jokes;
    $.getJSON('https://www.reddit.com/r/jokes.json', (json) => {
      _this.json = json;
      _this.json.data.children.forEach((element) => {
        const j = element.data.title;
        const p = element.data.selftext;
        const a = element.data.author;
        const l = element.data.permalink;
        _jokes.push({
          joke: j,
          punchline: p,
          author: a,
          link: l,
        });
      });
    });
  },
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
  min-height: 10vh;
  max-width: 70vh;
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

.author, .link {
  margin-top: 5px;
  font-size: 0.75rem;
  display: flex;
  align-self: flex-start;
}
</style>
