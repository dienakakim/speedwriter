<template>
  <div v-dompurify-html="textMD"></div>
</template>

<script>
import Vue from 'vue';
import VueDOMPurifyHTML from 'vue-dompurify-html';
Vue.use(VueDOMPurifyHTML);
import marked from 'marked';
export default {
  name: 'MarkdownPreview',
  components: {
    VueDOMPurifyHTML
  },
  props: {
    text: String
  },
  computed: {
    textMD() {
      return marked(this.$props.text);
    }
  }
};
</script>

<style>
@import url('../../assets/css/custom.css');
</style>
