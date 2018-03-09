<template>
    <div><p v-html='content'></p></div>
</template>

<script>
export default {
  data(){
    return{
      content: ''
    }
  },
  methods: {
    showChapter(c) {
      this.$set(this.$data, 'content', c);

      //回到顶部
      scrollTo(0,0);
    }
  }
}

</script>
