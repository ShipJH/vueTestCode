<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        
        <div id="app1" class="typo-line">
              <h1>호출성공</h1>
        </div>
        <button v-on:click="searchTerm">글 불러오기</button>

        <div v-for="(list, index) in boardList" :key="list.boardNo">
            <div><p> {{ index }} </p></div>
            <div><p>{{list.title}}</p></div>
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
        }
    },
    methods: {
        searchTerm: function () {
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
    }
  }

</script>
<style>

</style>
