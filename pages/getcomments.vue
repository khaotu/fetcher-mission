<template lang="html">
  <div class="back">
    <div class="box">
      <div class="head"><h1>Random Post</h1></div>
      <!-- <button
        @click="randomnum()">Go</button> -->
      <div class="click">
        <a
          @click="getnumber()">Random</a>
      </div>
      <div class="postid" v-show='PostId'>
        <h1>PostId:<h1 id="demo"></h1></h1>

      </div>
      <!-- <p> {{ 'https://jsonplaceholder.typicode.com/posts/' + random }} </p> -->
      <span class="post" v-show="titlepost">
        <h1>{{ 'Post: '+ post }}</h1>
      </span>
      <!-- <button
        @click="getcomment()">Show Comment</button> -->
        <div class="Load">
          <span v-show="load">
            Loading..
          </span>
        </div>
        <ul>
          <div class="in">
            <li
              v-for="post of comments"
              :key="post.id">
              <div class="info">
                <div class="id-txt"><p> {{ 'id '+ post.id }} </p></div>
                <div class="name-txt"><p><strong> {{ post.name }} </strong></p></div>
                <div class="txt"><p> {{ 'e-mail ' + post.email }} </p></div>
                <div class="txt"><p> {{ 'comment ' + post.body }} </p></div>
              </div>
            </li>
          </div>
        </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      random: Number,
      post: String,
      posts: [],
      comment: String,
      comments:[],
      PostId: false,
      load: false,
      titlepost: false,
    };
  },
  methods: {
    randomnum(){
      var x = document.getElementById("demo")
      x.innerHTML = Math.floor((Math.random() * 100) + 1);
      this.random = x.innerHTML;
      this.PostId = true;
    },
    getnumber() {
      this.load = true;
      this.posts = [];
      this.random = Number;
      this.titlepost = false;
      this.PostId = false,
      this.comments = [];
      setTimeout(() => {
        // this.load = false;
      var x = document.getElementById("demo")
      x.innerHTML = Math.floor((Math.random() * 100) + 1);
      this.random = x.innerHTML;
      this.PostId = true;
      this.titlepost = true;

        axios.get('https://jsonplaceholder.typicode.com/posts/' + this.random)
          .then((response) => {
            this.posts = response.data;
            console.log(this.posts);
            this.load = false;
            this.post = response.data.title;
            // alert('Found ' + this.posts.length + ' items')
            this.comment = 'https://jsonplaceholder.typicode.com/posts/' + this.random;
            axios.get(this.comment + '/comments')
              .then((response) => {
                this.comments = response.data;
                console.log(this.posts);
                alert('Found ' + this.comments.length + ' items')
                // this.comments = response.data.name;
              })
              .catch((e) => {
                this.text = e.message;
                // alert(e.message);
                this.popup = true;
                // this.error = true;
              });

          })
      }, 1000);
  },
}
}
</script>

<style lang="css" scoped>
ul {
  list-style-type: none;
}
.info {
  width       : 60vw;
  height      : 160px;
  margin-top  : 10px;
  margin-left : 1vw;
  background  : #c68400;
  border      : 3px solid #fff ;
}
.box {
  width       : 70vw;
  height      : auto;
  margin-left : 15vw;
  margin-top  : 50px;
  background  : #F6BB42;
}
.head {
  font-size   : 3em;
  margin-left : 50px;
  color       : #40241a;
}
.click {
  display           : flex;
  justify-content   : center;
  align-items       : center;
  margin-left       : 20vw;
  margin-top        : 20px;
  font-size         : 2em;
  width             : 400px;
  height            : 50px;
  background        : white;
  border-radius     : 100px;
  border            : 3px solid #c68400;
  margin-bottom     : 30px;
}
.Load {
  font-size         : 2em;
  margin-left: 20px;
}
.post ,.postid {
  margin-left: 20px;
}
.txt {
  margin-left: 1vw;
}
.id-txt {
  margin-left: 100px;
  margin-top: 15px;
  font-size: 1.3em;
}
.name-txt {
  margin-left: 3vw;
  margin-bottom: 10px;
}
@media only screen and (max-width: 1024px) {
  .info {
    width       : 70vw;
    height      : 180px;
    margin-top  : 10px;
    margin-left : 1vw;
    background  : #c68400;
    border      : 3px solid #fff ;
  }
  .box {
    width       : 80vw;
    height      : auto;
    margin-left : 10vw;
    margin-top  : 50px;
    background  : #F6BB42;
  }
}
@media only screen and (max-width: 690px) {
  .box {
    width       : 90vw;
    height      : auto;
    margin-left : 5vw;
    margin-top  : 50px;
    background  : #F6BB42;
  }
  .info {
    width       : 80vw;
    margin-left : -1vw;
  }
  .click {
    height            : 50px;
  }
}
@media only screen and (max-width: 580px) {
  click {
    margin-left       : -10vw;
    width             : 95vw;
  }
}
@media only screen and (max-width: 414px) {
  .box {
    width       : 100vw;
    height      : auto;
    margin-left : 0vw;
    margin-top  : 0px;
  }
  .click {
    margin-left       : 2vw;
    width             : 95vw;
  }
  .info {
    width       : 95vw;
    height      : 200px;
    margin-top  : 10px;
    margin-left : -7vw;
    background  : #c68400;
    border      : 3px solid #fff ;
  }
}
</style>
