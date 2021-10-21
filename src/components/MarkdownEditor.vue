<template>
  <div>
    <textarea :value="markdownContent" @input="handleMarkdownChange"></textarea>
  </div>
  <div id="generated_html" v-html="generatehtml"></div>
</template>

<script>
var showdown = require("showdown"),
  showdownHighlight = require("showdown-highlight"),
  cheerio = require('cheerio'),
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
      const parsedMD = "<div id='superuniqueboi'>" + converter.makeHtml(this.markdownContent) + "</div>"


      let $cherrio = cheerio.load(parsedMD)
      const allElements = $cherrio('#superuniqueboi').children().map(function(i,el){ return { htmlString: $cherrio(this).toString(), type: el.name }});
      console.log(allElements)
      // console.log(parsedMD)
      return parsedMD;
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

code{
padding: 1px 3px;
    background-color: hsla(0,0%,93%,.5);
}

pre code{
padding: 0;
    background-color: transparent;
}

table {
    border-spacing: 0;
        box-shadow: 0 2px 2px 0 rgb(0 0 0 / 14%), 0 1px 5px 0 rgb(0 0 0 / 12%), 0 3px 1px -2px rgb(0 0 0 / 20%);
}

th{
  min-width: 10rem;
    background-color: rgba(0,0,0,.54);
    color: #fff;
    vertical-align: top;
};

code.hljs {
  background-color: transparent;
}

td{
  padding: 5px
};
</style>