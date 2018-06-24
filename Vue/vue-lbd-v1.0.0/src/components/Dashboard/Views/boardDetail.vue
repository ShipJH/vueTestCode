<template>
  <div class="content">
    <div class="container-fluid">
      <div class="">
        
        <div id="app1" class="">
              <h1>게시판</h1>
        </div>

        <table>
            <tr>
                <th>제목</th>
                <th>등록자</th>
                <th>등록일자</th>
            </tr>
            <tr>
                <td>{{ boardDetail.title }}</td>
                <td>{{ boardDetail.regUser }}</td>
                <td>{{ boardDetail.regDate }}</td>
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

</style>