<template>
  <div>
    <el-dialog title="搜索结果" :visible.sync="dialogTableVisible" v-on:close='closeDialog' :fullscreen='true'>
      <el-table :data="bookData" size='medium' style='width: 100%;'>
        <el-table-column label='书名' align='center'>
          <template slot-scope='scope'>
            <el-button @click.native.prevent="selectBook(scope.row.indexUrl)" type="text" size='small'>{{scope.row.bookName}}</el-button>
          </template>
        </el-table-column>
        <el-table-column label='作者' prop='author' ></el-table-column>
        <el-table-column label='最新章节' prop='lastChapter' ></el-table-column>
        <el-table-column label='状态' prop='status' ></el-table-column>
      </el-table>
    </el-dialog>
  </div>

</template>

<script>
import axios from 'axios'
export default {
    data() {
      return {
        dialogTableVisible: false,
        bookData: []
      };
    },
    methods: {
      closeDialog: function(){
      },
      selectBook: function(url) {
        this.$set(this.$data, 'dialogTableVisible', false);
        this.$emit('selectBook', url);
      },
      openBookList: function(books) {
        this.$set(this.$data, 'dialogTableVisible', true);
        this.$set(this.$data, 'bookData', books);

      }
    }
  };
</script>
