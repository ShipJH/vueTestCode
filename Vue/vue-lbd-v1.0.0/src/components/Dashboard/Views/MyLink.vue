<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        
        <div id="app1" class="typo-line">
              <h1>호출성공</h1>
        </div>
        <button v-on:click="searchTerm">글 불러오기</button>

        <div>{{linkMsg}}</div>
      </div>
    </div>
  </div>
</template>
<script>

  export default {
    name: 'app1',
    data: function () {
        return {
            linkMsg: "hi"
        }
    },
    methods: {
        searchTerm: function () {
            //this.linkMsg = "bye"
        this.$http.get("http://localhost:8080/test/")
            .then((response)  =>  {
                //this.loading = false;
                this.linkMsg = response.data.testValue;
            }, (error)  =>  {
                this.loading = false;
            })

          
        }
    }
  }

</script>
<style>

</style>
