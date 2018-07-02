<template>
        <div id="app1" class="">
              <board-detail :bno="boardNo"/>
              <reply :bno="boardNo"/>
        </div>
</template>
<script>
  import reply from './reply.vue'
  import boardDetail from './boardDetail.vue'
  export default {
    name: 'app1',
    components:{
        'reply': reply,
        'boardDetail': boardDetail
    },
    data: function () {
        return {
            component: 'reply',
            component: 'boardDetail',
            boardNo: this.$route.query.boardNo
        }
        
    }
  }

</script>
<style>

</style>