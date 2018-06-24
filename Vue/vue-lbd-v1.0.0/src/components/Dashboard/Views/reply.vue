<template>
      <div class="container">
      <div class="row">
         <div class="col-lg-5 offset-lg-4 col-12 comment-main rounded">
          <ul class="p-0" v-for="reply in replys" :key="reply.replyNo">
            <li>
                <div class="row comment-box p-1 pt-3 pr-4">
		        <div class="col-lg-2 col-3 user-img text-center">
                    		{{ reply.replyNo }}
                  	</div>
                  <div class="col-lg-10 col-9 user-comment bg-light rounded pb-1">
                       <div class="row">
                             <div class="col-lg-8 col-6 border-bottom pr-0">
                                <p class="w-100 p-2 m-0">{{ reply.content }}</p>
                             </div>
                             <div class="col-lg-4 col-6 border-bottom">
                                <p class="w-100 p-2 m-0"><span class="float-right"><i class="fa fa-clock-o mr-1" aria-hidden="true"></i>01 : 00</span></p>
                             </div>
                       </div>
                      <div class="user-comment-desc p-1 pl-2">
                          <a href="#" class="m-0 mr-2" @click.prevent="replyInsertForm(reply.replyNo)">comment</a>
                      </div>  
                  </div>
                </div>
            </li>
            <div class="test" v-bind:id="'reply'+reply.replyNo">
            <br>
            <div class="row">
              <div class="col-lg-10 col-10">
                <input type="text" class="form-control" placeholder="write comments ..." v-model="replyContent.content">
              </div>
              <div class="col-lg-2 col-2 send-icon">
                <a href="#" @click.prevent="replyInsert" target="_blank"><i class="fa fa-paper-plane" aria-hidden="true"></i></a>
              </div>
            </div>
            </div>
            </ul>
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
       replyInsertForm(replyNo){
           var id = "reply"+replyNo;
           var form =document.getElementById(id);
           if (form.style.display === "none") {
                form.style.display = "block";
           } else {
                form.style.display = "none";
        }
       }
    }
  }
</script>
<style>
.comment-main ul{
	list-style: none;
}
.sub-cmt-img{
	width: 55px !important;
    height: 55px !important;
    border-radius: 50%;
} 
.main-cmt-img{
    width: 40px !important;
    height: 40px !important;
    border-radius: 50%;
}

.border-bottom{
	font-size: 13px;
	border-bottom: 1px solid #d3d3d3;
}
.user-comment{
	background-color: #bae6e9 !important;
    box-shadow: 0px 5px 8px -4px #c1c1c1;
}
.user-comment-desc{
    font-size: 5px;
	color: #a0a0a0;
}
.user-comment-desc p{
	font-size: 12px;
	display: inline-block;
	/* float: left; */
}
.send-icon i{
	font-size: 20px;
	background: #d7eef0;
	padding: 6px 5px;
	border-radius: 50%;
	color: #74C2E1;
	height: 35px;
	width: 35px;
}
.test{
    display:none;
}
</style>
