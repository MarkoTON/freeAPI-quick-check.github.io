<template>
  <div id="app" class="container-fluid">
    <h1 class="text-center border-bottom">Free API fast check: {{ linkTitle }}</h1>
    <div class="row">
      <div class="col-12 col-md-4 mb-4 mb-md-0">
        <Home @iframeInfo="addIframe" />
      </div><!-- col-2 col-md-3 -->
      <div class="col-12 col-md-8">
        <LinkValue :linkIframe="linkPick" />
      </div><!-- col-2 col-md-3 -->
    </div><!-- row -->
  </div>
</template>

<script>
import Home from './components/Home'
import LinkValue from './components/LinkValue'

export default {
  name: 'App',
  data(){
    return {
      linkTitle: 'Cat Facts',
      linkPick: 'https://alexwohlbruck.github.io/cat-facts/'
    }
  },
  components: {
    Home,
    LinkValue
  },
  methods: {
    addIframe(payload){
      this.linkPick = payload.info;
      this.linkTitle = payload.titleInfo;
    }
  }
}
</script>

<style>

</style>
