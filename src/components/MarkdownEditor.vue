<template>
  <div>
    <textarea :value="markdownContent" @input="handleMarkdownChange"></textarea>
  </div>
  <div id="generated_html" v-html="generatehtml"></div>
</template>

<script>
var showdown = require("showdown"),
  showdownHighlight = require("showdown-highlight"),
  converter = new showdown.Converter({
    tables: true,
    extensions: [
      showdownHighlight
    ],
  });

export default {
  name: "MarkdownEditor",
  props: {
    markdownContent: String,
  },
  methods: {
    handleMarkdownChange(event) {
      this.$emit("update-markdown", event.target.value);
    },
  },
  emits: ["update-markdown"],
  computed: {
    generatehtml() {
      console.log("Rerendering");
      return converter.makeHtml(this.markdownContent);
    },
  },
};
</script>

<style>
textarea {
  height: 100%;
  width: 100%;
  padding: 0;
  margin: 0;
}

div {
  width: calc(50vw - 30px);
}

#generated_html {
  border: 1px solid black;
  padding: 0 10px;
}

.hljs-keyword{
  color: #CC7832;
  
}

.hljs-meta{
  color: #BBB529;
}

pre{
  background-color: #2B2B2B;
  padding: 5px;
  border-radius: 5px;
}

.hljs-string{
  color: #6A8759;
}

.hljs-class{
  color: #A9B7C6;
}

.hljs-class > .hljs-title{
    color: #A9B7C6;

}

.hljs-function{
    color: #A9B7C6;

}

.hljs-function > .hljs-title{
    color: #FFC66D;

}
code.hljs {
  color: #A9B7C6
}
</style>