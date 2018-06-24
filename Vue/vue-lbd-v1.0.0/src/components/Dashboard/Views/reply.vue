<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        
        <div id="app1" class="typo-line">
        <input type="text" v-model="test.content"/>
        <button v-on:click="replyInsert">댓글작성</button>
        <ul v-for="(reply,index) in replys" :key="reply.replyNo">
            <li>{{ reply.replyNo }} , {{ reply.boardNo }} , {{ reply.content }} , {{ reply.replyGroup }} , {{ reply.useYn }} , <input type="button" value="댓글작성2" v-on:click="add(index, reply.replyNo)"/>
             <div v-bind:id="'reply'+reply.replyNo"></div>
            </li>
        </ul>
        <test1/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import test from './UserProfile/test.vue'
  import test1 from './UserProfile/test1.vue'
  export default {
    components:{
        'test':test,
        'test1':test1
    },
    name: 'app1',
    data(){
        return{
        replys:[],
        test:{},
        a:{},
        component: 'test1',
        aa: {}
        }

    },
    created: function(){
            this.replyData();
            console.log(this.$route.query.boardNo);
    },
    methods: {
        replyData: function () {
            //this.linkMsg = "bye"
        this.$http.get("http://localhost:8080/board/4020/")
            .then((response)  =>  {
                //this.loading = false;
                this.replys = response.data.replyList;
            }, (error)  =>  {
                this.loading = false;
            })
        },
       replyInsert: function () {
       this.$http.post("http://localhost:8080/board/4021/", this.test )
           .then((response)  =>  {
               //this.boardList = response.data.replyList;
               //this.loading = false;
               //this.linkMsg = response.data.testValue;
               this.replyData();
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
