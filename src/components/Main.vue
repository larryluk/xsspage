<template>
  <el-container>
    <el-header>
      <head-compment ref='head' v-on:getChapter='getChapter' v-on:searchBook='searchBook'></head-compment>
    </el-header>

    <el-main>
      <content-compment ref='content' :child-msg='chapter'></content-compment>
    </el-main>

    <el-footer>
      <foot-compment ref='foot' v-on:showChapter='getChapter' v-on:index='indexList'></foot-compment>
    </el-footer>

  <index-list ref='indexList' v-on:loadChapter='loadChapter'></index-list>
  <book-list ref='bookList' v-on:selectBook='selectBook'></book-list>
  </el-container>

</template>

<script>
import head from './Head.vue'
import content from './Content.vue'
import foot from './Foot.vue'
import indexList from './IndexList.vue'
import bookList from './BookList'
import axios from 'axios'

export default {
  dara(){
    chapter: ''
  },
  methods: {
    loadChapter: function(url) {
      var _this = this;
      axios.get('getXsChapter?url=' + url)
        .then((resp) => {
          _this.getChapter(resp.data.data);
      });
    },
    getChapter: function(c) {
        this.$set(this.$data, 'chapter', c);
        this.$refs.head.changeTitle(c.title);
        this.$refs.content.showChapter(c.content);
        this.$refs.foot.changeChapter(c.prevUrl, c.nextUrl, c.index);
    },
    indexList: function(url) {
      this.$refs.indexList.switchDialog(url);
    },
    searchBook: function(key) {
      var _this = this;
      axios.get('/searchXs?key=' + key)
        .then((resp) => {
          var result = resp.data;
          if(result.code == '10') {
            this.$refs.indexList.showDialog(result.data);
          } else if (result.code == '11') {
            this.$refs.bookList.openBookList(result.data);
          } else {
            this.$notify.error({
              title: '暂无数据',
              message: '暂无相关书籍信息'
            });
          }
        });
    },
    selectBook: function(url) {
      this.indexList(url);
    }
  },
  components: {
    'head-compment': head,
    'content-compment': content,
    'foot-compment': foot,
    'index-list': indexList,
    'book-list': bookList
  }
}
</script>
