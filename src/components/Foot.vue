<template>
    <el-button-group>
      <el-button type="primary" @click='prevChapter' icon="el-icon-arrow-left">上一页</el-button>
      <el-button type="primary" icon="el-icon-tickets" @click='indexList' >目录</el-button>
      <el-button type="primary" @click='nextChapter' >下一页<i class="el-icon-arrow-right el-icon--right"></i></el-button>
    </el-button-group>
</template>

<style>
#foot {
  width: 100%;
  height: auto;
  display: -webkit-inline-box;
  float:left;
  background: azure;
}

#prev {
  width: 33.3%;
  height: auto;
}

#index {
  width: 33.3%;
  height: auto;
}

#next {
  width: 33.3%;
  height: auto;
}
</style>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      next: '',
      prev: '',
      index: ''
    }
  },
  methods: {
    changeChapter: function(prev, next, index) {
      this.$set(this.$data, 'next', next);
      this.$set(this.$data, 'prev', prev);
      this.$set(this.$data, 'index', index);
      console.log('changeChapter');
    },
    getChapter: function(url) {
      var _this = this;
      axios.get('getXsChapter?url=' + url)
        .then((resp) => {
            console.log(resp);
            _this.$emit('showChapter',resp.data.data);
      });
    },
    prevChapter: function() {
      this.getChapter(this.$data.prev);
    },
    nextChapter: function() {
      this.getChapter(this.$data.next);
    },
    indexList: function() {
      this.$emit('index', this.$data.index);
    }
  }
}
</script>
