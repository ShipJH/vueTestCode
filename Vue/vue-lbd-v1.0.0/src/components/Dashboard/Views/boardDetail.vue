<template>
	<div class="main-section">  
		<div class="content">
				<div class="user-detail">
					<p>{{ boardDetail.title }}</p>
					<span>{{ boardDetail.regDate }}</span>
				</div>		
			<div class="comment-content">
				<span>{{ boardDetail.content }}</span>
			</div>
		</div>
	</div>
</template>
<script>

  export default {
    name: 'app1',
    props: [
    'bno'
    ],
    data: function () {
        return {
            boardDetail: []
            // ,inputMyName:''
        }
        
    },
    created: function(){
            this.findByBoardList(this.bno);
    },
    methods: {
        findByBoardList: function (no) {
            //this.linkMsg = "bye"
        this.$http.get(this.$appUrl+"/board/4012/" + no)
            .then((response)  =>  {
                this.boardDetail = response.data;
                //this.loading = false;
                //this.linkMsg = response.data.testValue;
                
            }, (error)  =>  {
                this.loading = false;
            })

          
        }
    }
  }

</script>
<style>

.main-section{
	width: 35%;
	/* margin: 0 auto; */
}
.content{
	padding:20px;
}
.user-detail p{
	font-size:17px;
	font-weight:600;
	letter-spacing:1.5px;
	margin:15px 0px 10px 0px; 
}
.user-detail span{
	color:#a2a2a2;
}
.comment-content{
	margin-top:10px;
}
</style>