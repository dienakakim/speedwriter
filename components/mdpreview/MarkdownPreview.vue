<template>
  <div v-dompurify-html="$md.render(text)"></div>
</template>

<script>
import Vue from 'vue';
import VueDOMPurifyHTML from 'vue-dompurify-html';
Vue.use(VueDOMPurifyHTML);
export default {
  name: 'MarkdownPreview',
  components: {
    VueDOMPurifyHTML
  },
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
