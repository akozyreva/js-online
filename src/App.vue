<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />-->
    <div class="js-online-wrapper">
      <div class="editor-wrapper">
        <p>CSS</p>
        <textarea v-model="cssCode" rows="10" cols="100"></textarea>
      </div>
      <div class="editor-wrapper">
        <p>Js</p>
        <textarea v-model="jsCode" rows="10" cols="100"></textarea>
      </div>
      <div class="editor-wrapper">
        <p>html</p>
        <textarea v-model="htmlCode" rows="10" cols="100"></textarea>
      </div>
    </div>
    <div>
      <iframe id="finalIframe"> </iframe>
    </div>
    <button @click="addContent()">Run</button>
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
      htmlCode: "",
      cssCode: "",
      jsCode: ""
    };
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

.editor-wrapper {
  margin: 0;
  width: 50%;
}
</style>
