<template>
  <div v-html="$md.render(text)"></div>
</template>

<script>
export default {
  name: 'MarkdownPreview',
  props: {
    text: String
  },
  computed: {
    someMarkdown() {
      return someMarkdown;
    }
  }
};
</script>

<style>
@import url('../../assets/css/custom.css');
</style>
