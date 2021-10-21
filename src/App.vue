<template>
  <main>
    <markdown-editor :markdown-content="markdown" @update-markdown="updateMd" />
  </main>
</template>

<script>
import MarkdownEditor from "./components/MarkdownEditor.vue";

export default {
  name: "App",
  components: {
    MarkdownEditor,
  },
  data() {
    return {
      markdown: `# Hello World`,
    };
  },
  methods: {
    updateMd(newMD) {
            // console.log("Before",this.markdownValue);

      this.markdown = newMD;
      // console.log("After",this.markdownValue);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  width: 100%;
  height: 100%;
}

body {
  width: 100vw;
  min-height: 50vh;
  margin: 0;
  padding: 0;
}
main {

  display: flex;
    flex-direction: row;
    justify-content: space-around;
}

p{
  font-size: 1em;
}
</style>
