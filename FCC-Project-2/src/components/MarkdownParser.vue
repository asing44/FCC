<script setup lang="ts">
  import { ref } from 'vue';
  import { marked } from 'marked';

  const text = ref(`# Welcome to my React Markdown Previewer!

## This is a sub - heading...
### And here's some other cool stuff:

Heres some code, \`<div></>\`, between 2 backticks.

\`\`\`
  // this is multi-line code:
  function anotherExample(firstLine, lastLine) {
    if (firstLine == '' && lastLine == '') {
      return multiLineCode;
    }
  }
\`\`\`

You can also make text **bold**...whoa!
Or _italic_.
Or...wait for it... **_both!_**
And feel free to go crazy ~~crossing stuff out~~.

There's also [links](https://www.freecodecamp.org), and
> Block Quotes!

And if you want to get really crazy, even tables:

| Wild Header | Crazy Header | Another Header? |
| ----------- | ------------ | --------------- |
| Your content can | be here, and it | can be here.... |
| And here. | Okay. | I think we get it. |

- And of course there are lists.
  - Some are bulleted.
    - With different indentation levels.
      - That look like this.

1. And there are numbered lists too.
1. Use just 1s if you want!
1. And last but not least, let's not forget embedded images:

![freeCodeCamp Logo](https://cdn.freecodecamp.org/testable-projects-fcc/images/fcc_secondary.svg)
`);

  marked.setOptions({
    renderer: new marked.Renderer(),
    gfm: true,
    breaks: true,
    pedantic: false,
    // sanitize: true,
    // smartLists: true,
    // smartypants: true
  });

</script>

<template>
  <div class="container">
    <textarea id="editor" class="input" type="input" placeholder="Enter Markdown here..." v-model="text" />
    <div id="preview" class="output" v-html=" marked(text) "></div>
  </div>
</template>

<style>
.output {
  border: 1px solid #ddd;
  padding: 10px;
  margin-top: 10px;
  color: black;
  text-align: left;
}

.input {
  padding: 10px 15px;
  width: 100%;
  height: 150px;
}
</style>
