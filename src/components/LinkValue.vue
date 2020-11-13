<template>
  <div>
    <div style="height:93vh" class="bg-info">
      <iframe :src="linkIframe" frameborder="0" width="100%" height="100%"></iframe>
    </div>
  </div>
</template>
<script>
export default {
  name:"LinkValue",
  props:['linkIframe'],
  data(){
    return {

    }
  }
};
</script>
<style scoped>

</style>