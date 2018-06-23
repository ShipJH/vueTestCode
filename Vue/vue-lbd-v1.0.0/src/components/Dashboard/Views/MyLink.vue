<template>
  <div class="content">
    <div class="container-fluid">
      <div class="">
        
        <div id="app1" class="">
              <h1>게시판</h1>
        </div>

        <table>
            <tr>
                <th>No</th>
                <th>제목</th>
                <th>등록자</th>
                <th>등록일자</th>
            </tr>
            <tr v-for="(list, index) in boardList" :key="list.boardNo">
                <td>{{ index + 1 }}</td>
                <td><a v-on:click="goDetail(list.boardNo)">{{ list.title }}</a></td>
                <td>{{ list.regUser }}</td>
                <td>{{ list.regDate }}</td>
            </tr>
        </table>
        <!-- <input type="text" v-model="inputMyName"/> -->
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
        this.$http.get("http://localhost:8080/board/4010/")
            .then((response)  =>  {
                this.boardList = response.data.boardList;
                //this.loading = false;
                //this.linkMsg = response.data.testValue;
                
            }, (error)  =>  {
                this.loading = false;
            })

          
        }
        ,
        goDetail: function(No) {
            alert(No);
            this.$router.push({name: 'reply', params: { foo: "bar"}});
        }
    }
  }

</script>
<style>

</style>
