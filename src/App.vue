<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />-->
    <div>
      <p>CSS</p>
      <textarea v-model="cssCode" rows="10" cols="50"></textarea>
    </div>
    <div>
       <p>Js</p>
      <textarea v-model="jsCode" rows="10" cols="50"></textarea>
    </div>
    <div>
      <p>html</p>
      <textarea v-model="htmlCode" rows="10" cols="50"></textarea>
    </div>
    
    <button @click="addContent()">Run</button>
    <iframe id="finalIframe">
    </iframe>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "app",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      htmlCode: '',
      cssCode: '',
      jsCode: 'aa'
    }
  },
  methods: {
    addContent() {
      let x = document.getElementById("finalIframe").contentWindow.document;
      x.open();
      console.log(this.htmlCode, this.jsCode)
      x.write(this.htmlCode);
      x.write(`<script>${this.jsCode}<\/script>`)
      x.close();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
