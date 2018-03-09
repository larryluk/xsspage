<template>
  <div>
    <el-dialog title="目录" :visible.sync="dialogTableVisible" v-on:close='closeDialog' :fullscreen='true'>
      <el-switch v-model="order" active-text="倒序" inactive-text="正序" @change='changeOrder'></el-switch>
      <el-table :data="chapterData" size='medium'>
        <el-table-column align='center'>
          <template slot-scope='scope'>
            <el-button @click.native.prevent="selectChapter(scope.row.url)" type="text" size='small'>{{scope.row.title}}</el-button>
          </template>
        </el-table-column>
      </el-table>
      <el-button-group>
        <el-button type="primary" @click='loadChapter'>加载更多</el-button>
        <el-button @click='dialogTableVisible = false'>关闭</el-button>
      </el-button-group>
    </el-dialog>
  </div>

</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      order: false,
      chapterData: [],
      allChapterData:[],
      pageNo: 1,
      pageSize: 15,
      dialogTableVisible: false,
    };
  },
  methods: {
    switchDialog: function(url) {
      var resful = '/getXsIndex?url=' + url;
      axios.get(resful)
        .then((resp) => {
        this.$set(this.$data, 'allChapterData', resp.data.data);
        this.$set(this.$data, 'dialogTableVisible', true);
        this.loadChapter();
      });
    },
    showDialog: function(chapterData) {
        this.$set(this.$data, 'allChapterData', chapterData);
        this.$set(this.$data, 'dialogTableVisible', true);
        this.loadChapter();
    },
    selectChapter: function(url) {
      this.$emit('loadChapter', url);
      this.$set(this.$data, 'dialogTableVisible', false);
    },
    changeOrder: function(value) {
      var reverse = this.$data.allChapterData.reverse();
      this.$set(this.$data, 'allChapterData', reverse);
      this.$set(this.$data, 'pageNo', 1);
      this.$set(this.$data, 'chapterData', []);
      this.loadChapter();
    },
    loadChapter: function() {
      var pageNo = this.$data.pageNo;
      var pageSize = this.$data.pageSize;

      var start = (pageNo - 1) * pageSize;
      var loadChapter = this.$data.chapterData;
      for(var i = 0; i < pageSize; i++) {
        loadChapter.push(this.$data.allChapterData[start + i]);
      }

      //增加页数
      this.$set(this.$data, 'pageNo', pageNo + 1);
      this.$set(this.$data, 'chapterData', loadChapter);
    },
    closeDialog: function(){
      this.$set(this.$data, 'pageNo', 1);
      this.$set(this.$data, 'chapterData', []);
      this.$set(this.$data, 'order', false);
    }
  }
};
</script>
