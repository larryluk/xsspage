<template>
    <div id='head'>
      <div id='menu' v-on:click='openMenu'><img src='../../static/img/menu.png'></img></div>
      <div id="title">{{title}}</div>
      <div id="person"><img src="../../static/img/person.png"></img></div>
      <div><nav-components ref='nav' v-on:showChapter='showChapter' v-on:searchBook='searchBook'></nav-components></div>
    </div>
</template>

<script>
import nav from './Nav.vue'
export default {
  data() {
    return {
      title: '章节标题'
    }
  },
  methods: {
    openMenu: function() {
      this.$refs.nav.menuSwitch(true);
    },
    showChapter: function(data) {
      this.$emit('getChapter', data);
    },
    changeTitle: function(title) {
      this.$set(this.$data, 'title', title);
      this.$refs.nav.menuSwitch(false);
    },
    searchBook: function(key) {
      this.$emit('searchBook', key);
    }
  },
  components: {
    'nav-components': nav
  }
}
</script>

<style>
#head {
  width: 100%;
  height: auto;
  display: -webkit-inline-box;
  float:left;
  background: azure;

}

#menu {
  width:10%;
  height: 100%;
}

#menu img {
  width: 30px;
}

#person img {
  width: 30px;
}

#title {
  width: 80%;
  height: auto;
  text-align:center;
}

#person {
  width:10%;
  height: auto;
}


</style>
