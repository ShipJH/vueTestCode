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
                    <tr v-for="(list, index) in boardList" :key="list.boardNo" v-on:click="goDetail(list.boardNo)" style="cursor:pointer;">
                        <td>{{ list.boardNo }}</td>
                        <td>{{ list.title }}</td>
                        <td>{{ list.regUser }}</td>
                        <td>{{ list.regDate }}</td>
                        <td><input type="button" v-on:click="addRow(index)" value="인덱스테스트"/></td>
                    </tr>
                </tbody>
            </table>

             <a href="#" :key="n" v-on:click="goPage(n)" v-for="n in listCnt">{{ n }} </a>

             
            
        </div>
        
        <a href="#" :key="n" v-on:click="goPage(n+5)"  v-for="n in 5">{{ n+5 }} </a>
        <br/>
        <a href="#" :key="n" v-on:click="goPage(n+10)"  v-for="n in 5">{{ n+10 }} </a>

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

            listCnt:0,
            pageNo:1,
            n:11



            
            // ,inputMyName:''
        }
         
    },
    created: function(){
            this.findByBoardList();
            this.searchSelect = "ALL";
    },
    methods: {

        goPage: function(n){
            console.log(n);
            this.$http.get(this.$appUrl+"/board/4010/01/"+n+"/제")
                .then((response)  =>  {
                    this.boardList = response.data.boardList;

                    this.listCnt = response.data.listCnt;
                    //this.loading = false;
                    //this.linkMsg = response.data.testValue;
                    
                }, (error)  =>  {
                    this.loading = false;
                })
        },

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

                    this.listCnt = response.data.listCnt;
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
        },
        addRow(index){
            alert(index);
        }
    }
  }

</script>
<style>

</style>