<template>
  <main>
    <section>
    <markdown-editor :markdownContent="markdown" @update-markdown="updateMd" />
    </section>
    <section>
    <markdown-displayer :markdownContent="markdown" />
    </section>
  </main>
</template>

<script>
import MarkdownEditor from "./components/MarkdownEditor.vue";
import MarkdownDisplayer from "./components/MarkdownDisplayer.vue"

export default {
  name: "App",
  components: {
    MarkdownEditor,
    MarkdownDisplayer
  },
  data() {
    return {
      markdown: `# Hello World`,
    };
  },
  methods: {
    updateMd(updatedMarkdown) { 
      this.markdown = updatedMarkdown;
    },
        say(message) {
      alert(message)
    }
  }
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
    -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}
main {

  display: flex;
    flex-direction: row;
    justify-content: flex-start;
}

p{
  font-size: 1em;
}

section{
  width: 50vw;
}

body::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for IE, Edge and Firefox */
body {

}
</style>
