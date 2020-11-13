<template>
  <div class="hello">
    <input placeholder="Search by Description" type="text" class="form-control mb-2" v-model="searchByTitle">
    <div style="height:89vh; overflow-y: auto;">
      <ul @click="showInfo(data.Link)" class="list-group clickable" v-for="(data,index) in filteredLinks()" :key="index">
        <li class="list-group-item mb-1">
          <span>API: {{data.API}}</span><br>
          <span>Description: {{data.Description}}</span><br>
          <span>Auth: {{data.Auth}}</span><br>
          <span>HTTPS: {{data.HTTPS}}</span><br>
          <span>Cors: {{data.Cors}}</span><br>
          <span>Link: <a :href="data.Link" target="_blank">{{data.Link}}</a></span><br>
          <span>Category: {{data.Category}}</span><br>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import jikanjs from 'jikanjs';
import axios from 'axios';

export default {
  name: 'Home',
  data () {
    return {
      info:[],
      searchByTitle: ''
    }
  },
  beforeCreate(){
    axios
    .get('https://api.publicapis.org/entries')
    .then(response => {
        return this.info = response.data.entries
    })
  },
  methods: {
    showInfo(info){
      console.log(info);
      this.$emit('iframeInfo',{ info:info })
    },
    filteredLinks(){
      return this.info.filter(infoTitle => {
        // console.log(infoTitle.API);
        return infoTitle.Description.toLowerCase().match(this.searchByTitle)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.clickable {
  cursor: pointer;
}
</style>
