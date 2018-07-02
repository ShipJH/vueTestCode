<template>
  <div class="content">
    <div class="container-fluid">
      <div class="">
        
        
        <h2><i class="nc-icon nc-notes" /> Community<br/></h2>
        <h6>Community > 자유게시판</h6>

        <div class="row">
            <div class="col-md-3">
                셀렉트박스 들어갈 곳
            </div>

            <div class="col-md-9">
                <input aria-describedby="addon-right addon-left" type="text" placeholder="Search" class="form-control">
            </div>
        </div>
        

        <div class="table-responsive">
            <table class="table table-hover" >
                <thead>
                        <th>No</th>
                        <th>제목</th>
                        <th>등록자</th>
                        <th>등록일자</th>
                </thead>
                <tbody>
                    <tr v-for="(list, index) in boardList" :key="list.boardNo" v-on:click="goDetail(list.boardNo)" style="cursor:pointer;">
                        <td>{{ index + 1 }}</td>
                        <td>{{ list.title }}</td>
                        <td>{{ list.regUser }}</td>
                        <td>{{ list.regDate }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

  export default {
    name: 'app1',
    data: function () {
        return {
            boardList: []
            // ,inputMyName:''
        }
        
    },
    created: function(){
            this.findByBoardList();
    },
    methods: {
        findByBoardList: function () {
            //this.linkMsg = "bye"
        this.$http.get(this.$appUrl+"/board/4010/")
            .then((response)  =>  {
                this.boardList = response.data.boardList;
                //this.loading = false;
                //this.linkMsg = response.data.testValue;
                
            }, (error)  =>  {
                this.loading = false;
            })

          
        }
        ,
        goDetail: function(no) {
            this.$router.push({name: 'detailView', query: { boardNo: no}});
        }
    }
  }

</script>
<style>

</style>