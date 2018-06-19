<template lang="html">
  <div>
    <div class="header">
      <h1>Data</h1>
    </div>
    <span v-show="load">
      Loading
    </span>
    <span v-show="example">
      <button
        @click="getdata()">Greet</button>
    </span>
    <div id="ex_error">
      <button
        @click="geterror()">Go</button>
    </div>
    <div v-show="popup">
      <pop :txt="text"/>
    </div>
    <div>
      <h1>Hello</h1>
      <ul>
        <div class="in">
          <li
            v-for="post of posts"
            :key="post.name">
            <div class="info">
              <p><strong> {{ post.name }} </strong></p>
              <p> {{ post.username }} </p>
              <p> {{ post.email }} </p>
            </div>
          </li>
        </div>
      </ul>

    </div>
  </div>

</template>

<script>
import axios from 'axios';
import popup from '~/components/popup.vue';

export default {
  components: {
    pop: popup,
  },
  data() {
    return {
      posts: [],
      errors: [],
      load: false,
      text: String,
      found: 'Found ',
      items: ' items',
      example: true,
      length: String,
      popup: false,
    };
  },
  // Fetches posts when the component is created.
  methods: {
    getdata() {
      this.load = true;
      this.example = false;
      this.posts = []
      setTimeout(() => {
        // alert('Timeout');
        this.load = false;
        this.example = true;
        axios.get('https://jsonplaceholder.typicode.com/users')
          .then((response) => {
            this.posts = response.data;
            console.log(this.posts);
            this.length = this.posts.length;
            this.text = this.found + this.posts.length + this.items;
            // alert(this.found + this.posts.length + this.items);
            this.popup = true;
          })
          .catch((e) => {
            this.error = this.errors.push(e);
            console.log(this.errors);
          });
      }, 1000);
    },
    geterror() {
      setTimeout(() => {
        // this.load = false;

        axios.get('https://reqres.in/api/unknown/23')
          .then((response) => {
            this.posts = response.data;
            console.log(this.posts);
            this.load = true;
          })
          .catch((e) => {
            // this.errors = this.errors.push(e);
            // this.error = this.errors.push(e.request.message);
            console.log(JSON.stringify(e));
            // this.text = e.message;
            // alert(e.message);
            // this.popup = true;
            // this.error = true;
          });

      }, 1000);
    },

  },
};
</script>

<style lang="css">
.info {
  width       : 300px;
  height      : 100px;
  margin-top  : 20px;
  background  : tomato;
}
.pop {
  width       : 100px;
  height      : 500px;
}

</style>
