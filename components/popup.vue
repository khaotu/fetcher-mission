<template lang="html">
  <div class="BG">
    <div v-show="popbox">
      <div class="box">
        <div class="font"><h1>{{ txt }}</h1></div>
        <div class="button"><button @click="close()">Close</button></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      popbox: true
    }
  },
  props: {
    txt: String,
  },
  methods: {

    close() {
      this.popbox = false;
    }
  }

};
</script>

<style lang="css" scoped>
.box {
  display         : flex;
  width           : 500px;
  height          : 300px;
  border          : 3px;
  background      : grey;
  position        : fixed;
  justify-content : center;
  align-items     : center;
  flex-direction  : column;
  margin          :10% 35%
}
.font {
  font-size       :0.8em;
  color           :white;
}
.BG {
  width           : 100vw;
  height          : 100vh;
  position        : fixed;
  /* border          : 1px solid tranparrent;
  opacity         : 0.6;
  filter          : alpha(opacity=70); */
}
.button {
  margin-top      :70px;
}
</style>
