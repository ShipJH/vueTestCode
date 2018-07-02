<template>
          <div class="col-md-13">
          <card>
            <template slot="header">
              <h5 class="title">comment</h5>
              <br/>
          <div class="row">
              <div class="col-md-8">
                <input type="text" class="form-control" placeholder="내용을 입력해주세요." v-model="replyContent.content"/>
              </div>
              <button @click.prevent="replyInsert" class="btn btn-info btn-fill float-right">작성</button>
          </div>
            </template>
            <l-table :data="replys">
                      <!-- :columns="replys.replyNo"> 
               <template slot="columns"></template> -->
              <template slot-scope="{row}">
                <td>{{row.replyNo}}</td>
                <td>{{row.content}}</td>
                <td class="td-actions text-right">
                  <button type="button" class="btn-simple btn btn-xs btn-info" v-tooltip.top-center="editTooltip">
                    <i class="fa fa-edit"></i>
                  </button>
                  <button type="button" class="btn-simple btn btn-xs btn-danger" v-tooltip.top-center="deleteTooltip">
                    <i class="fa fa-times"></i>
                  </button>
                </td>
              </template>
            </l-table>
          </card>

        </div>
</template>

<script>
  import Card from 'src/components/UIComponents/Cards/Card.vue'
  import LTable from 'src/components/UIComponents/Table.vue'
  export default {
    props: [
    'bno'
    ],
    components: {
      Card,
      LTable
    },
    name: 'app1',
    data(){
        return{
        replys:[],
        replyContent:{boardNo: this.bno},
        editTooltip: 'Add',
        deleteTooltip: 'Remove'
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

</style>