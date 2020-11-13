<template>
  <div class="hello">
    <input placeholder="Search by Description" type="text" class="form-control mb-2" v-model="searchByTitle">
    <div style="height:89vh; overflow-y: auto;">
      <div id="top"></div>
      <ul @click="showInfo(data.Link,data.API)" class="list-group clickable" v-for="(data,index) in filteredLinks()" :key="index">
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
      <a href="#top" v-smooth-scroll class="api-to-top text-info"><i class="fa fa-arrow-circle-up fa-3x"></i></a>
    </div>
  </div>
</template>

<script>
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
    showInfo(info,titleInfo){
      this.$emit('iframeInfo',{ info:info, titleInfo:titleInfo })
    },
    filteredLinks(){
      return this.info.filter(infoTitle => {
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

.api-to-top {
  position: absolute;
  z-index: 100;
  top: 80vh;
  left: 70vw;
}

@media only screen and (min-width: 320px) {
  .api-to-top {
    top: 70vh;
    left: 80vw;
  }
}

@media only screen and (min-width: 375px) {
  .api-to-top {
    top: 80vh;
  }
}

@media only screen and (min-width: 425px) {
  .api-to-top {
    left: 82vw;
  }
}

@media only screen and (min-width: 768px) {
  .api-to-top {
    top: 84vh;
    left: 23vw;
  }
}

@media only screen and (min-width: 1024px) {
  .api-to-top {
    top: 85vh;
    left: 24vw;
  }
}

@media only screen and (min-width: 1440px) {
  .api-to-top {
    left: 28vw;
  }
}
</style>
