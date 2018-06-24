<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        
        <div id="app1" class="typo-line">
        <input type="text" v-model="replyContent.content"/>
        <button v-on:click="replyInsert">댓글작성</button>
        <ul v-for="(reply,index) in replys" :key="reply.replyNo">
            <li>{{ reply.replyNo }} , {{ reply.boardNo }} , {{ reply.content }} , {{ reply.replyGroup }} , {{ reply.useYn }} , <input type="button" value="댓글작성2" v-on:click="add(index, reply.replyNo)"/>
             <div v-bind:id="'reply'+reply.replyNo"></div>
            </li>
        </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: [
    'bno'
    ],
    name: 'app1',
    data(){
        return{
        replys:[],
        replyContent:{boardNo: this.bno},
        a:{},
        aa: {}
        }

    },
    created: function(){
            this.replyData(this.bno);
    },
    methods: {
        replyData: function (no) {
            //this.linkMsg = "bye"
        this.$http.get("http://localhost:8080/board/4020/" + no)
            .then((response)  =>  {
                //this.loading = false;
                this.replys = response.data.replyList;
            }, (error)  =>  {
                this.loading = false;
            })
        },
       replyInsert: function () {
       this.$http.post("http://localhost:8080/board/4021/", this.replyContent )
           .then((response)  =>  {
               //this.boardList = response.data.replyList;
               //this.loading = false;
               //this.linkMsg = response.data.testValue;
               this.replyData(this.bno);
           }, (error)  =>  {
               this.loading = false;
           })

         
       },
       replyReset: function(id) {
           var test =document.getElementById(id);
           test.innerHTML="";
       },
       add: function(no, replyNo){
           var aa = 'reply'+replyNo;
           var test =document.getElementById(aa);
           test.innerHTML="<input type='text'/><button onClick='replyReset("+aa+")'>취소</button><button>등록</button>";
       }
    }
  }
</script>
<style>

</style>
