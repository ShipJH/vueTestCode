<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        
        <div id="app1" class="typo-line">
        <table border="1">
            <tr>
                <td>댓글번호</td>
                <td>게시글번호</td>
                <td>댓글내용</td>
                <td>댓글그룹번호</td>
                <td>댓글유효성여부</td>
            </tr>
            <tr v-for="reply in replys" v-bind:key="reply.replyNo">
                <td>{{ reply.replyNo }}</td>
                <td>{{ reply.boardNo }}</td>
                <td>{{ reply.content }}</td>
                <td>{{ reply.replyGroup }}</td>
                <td>{{ reply.useYn }}</td>
            </tr>
        </table>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

  export default {
    name: 'app1',
    data(){
        return{
        replys:[]
        }

    },
    created: function(){
            this.replyData();
    },
    methods: {
        replyData: function () {
            //this.linkMsg = "bye"
        this.$http.get("http://localhost:8080/board/4020")
            .then((response)  =>  {
                //this.loading = false;
                this.replys = response.data;
            }, (error)  =>  {
                this.loading = false;
            })
        }
    }
  }

</script>
<style>

</style>
