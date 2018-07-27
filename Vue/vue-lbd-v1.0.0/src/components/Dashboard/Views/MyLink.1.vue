<template>
  <div class="content">
    <div class="container-fluid">
      <div class="">
        
        
        <h2><i class="nc-icon nc-notes" /> Community<br/></h2>
        <h6>Community > 자유게시판</h6>

        <div class="row">
            <div class="col-md-3">
                <select v-model="searchSelect">
                    <option selected value="ALL">전체</option> 
                    <option value="01">제목</option>
                </select>
            </div>

            <div class="col-md-9">
                <input aria-describedby="addon-right addon-left" type="text" placeholder="Search" class="form-control" v-model="searchInput"  v-on:keyup="searchKeyUp" />
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
                    <tr v-for="(list) in boardList" :key="list.boardNo" v-on:click="goDetail(list.boardNo)" style="cursor:pointer;">
                        <td>{{ list.boardNo }}</td>
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
            boardList: [],
            searchInput:"",
            searchSelect:"",
            pageNo:1
            
            // ,inputMyName:''
        }
        
    },
    created: function(){
            this.findByBoardList();
            this.searchSelect = "ALL";
    },
    methods: {

        searchKeyUp : function(){
            this.findByBoardList();
        },

        findByBoardList: function () {
            //this.linkMsg = "bye"

            if(this.searchInput != ''){

            this.$http.get(this.$appUrl+"/board/4010/"+this.searchSelect+"/"+this.pageNo+"/"+this.searchInput)
                .then((response)  =>  {
                    this.boardList = response.data.boardList;
                    //this.loading = false;
                    //this.linkMsg = response.data.testValue;
                    
                }, (error)  =>  {
                    this.loading = false;
                })
            }else{
                this.$http.get(this.$appUrl+"/board/4010/01/1/제")
                .then((response)  =>  {
                    this.boardList = response.data.boardList;
                    //this.loading = false;
                    //this.linkMsg = response.data.testValue;
                    
                }, (error)  =>  {
                    this.loading = false;
                })
            }
          
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