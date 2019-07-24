<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-button @click="addContent()" variant="dark">Run</b-button>
      <b-row>
        <b-col sm="5" md="6"
          ><p>html</p>
          <textarea v-model="htmlCode" rows="10" cols="70"></textarea
        ></b-col>
        <b-col sm="5" md="6">
          <p>CSS</p>
          <textarea v-model="cssCode" rows="10" cols="70"></textarea>
        </b-col>
        <b-col sm="5" offset-sm="2" md="6" offset-md="0">
          <p>JS</p>
          <textarea v-model="jsCode" rows="10" cols="70"></textarea>
        </b-col>
        <b-col> <iframe id="finalIframe"> </iframe></b-col>
      </b-row>
    </b-container>
    <!--<img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />-->
    <div class="js-online-wrapper">
      <div class="editor-wrapper"></div>
      <div class="editor-wrapper"></div>
    </div>
    <div></div>
    <div id="logger"></div>
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
      htmlCode: "<p>Hello World!</p>",
      cssCode: "p { color: red; }",
      jsCode: " console.log('Things work!')"
    };
  },
  methods: {
    addContent() {
      let x = document.getElementById("finalIframe").contentWindow.document;
      x.open();
      console.log(this.htmlCode, this.jsCode);
      x.write(this.htmlCode);
      //console.log(this.jsCode.search('console.log'))
      x.write(`<script>${this.jsCode}<\/script>`);
      x.write(`<style>${this.cssCode}<\/style>`);
      x.close();
    }
  },
  mounted: function() {
    // Overriding console object
    var console = {};

    // Getting div to insert logs
    var logger = document.getElementById("logger");

    // Adding log method from our console object
    console.log = function(text) {
      var element = document.createElement("div");
      var txt = document.createTextNode(text);

      element.appendChild(txt);
      logger.appendChild(element);
    };
    // console.log(44444);
    this.addContent();
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
  background-color: #20262e;
}
</style>
