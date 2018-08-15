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
              <button @click.prevent="replyInsert()" class="btn btn-info btn-fill float-right">작성</button>
          </div>
            </template>
            
            <div class="table-responsive">
              <table class="table table-hover" >
                <template v-for="list in replys">
                    <tr :key="list.replyNo">
                        <td>{{list.replyNo}}</td>
                        <td>{{list.content}}</td>
                        <td class="td-actions text-right">
                        <!-- <button type="button" class="btn-simple btn btn-xs btn-info" v-tooltip.top-center="editTooltip" v-on:click="addRow(index)"> -->
                          <button type="button" class="btn-simple btn btn-xs btn-info" v-tooltip.top-center="editTooltip='Add'" @click="list.isReInsert = !list.isReInsert">
                          <i class="fa fa-edit"></i>
                        </button>
                        <button type="button" class="btn-simple btn btn-xs btn-danger" v-tooltip.top-center="deleteTooltip='Remove'" v-on:click="removeRow()">
                          <i class="fa fa-times"></i>
                        </button>
                        </td>
                    </tr>
                    <tr v-if="list.isReInsert" :key="list.replyNo">
                       <td>
                         <input type="text" class="form-control" placeholder="내용을 입력해주세요." v-model="replyContent.content"/>
                       </td>
                       <td>
                         <!-- <button @click.prevent="replyInsert" class="btn btn-info btn-fill float-right">작성</button> -->
                         <input type="button" value="작성" class="btn btn-info btn-fill float-right" @click="replyInsert(list.replyNo)">
                       </td>
                    </tr>
                    </template>
              </table>
            </div>

            <!-- <l-table :data="replys">
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
            </l-table> -->
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
        replyContent:{boardNo: this.bno, replyNo: 0}
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
       replyInsert: function (replyNo) {

        this.replyContent.replyNo=replyNo;

        const notification = {
          template: `<span>댓글 입력 성공!!</span>`
        }

        const notificationfalse ={
          template: `<span>댓글 입력 실패 ㅠㅠ</span>`
        }

       this.$http.post("http://localhost:8080/board/4021/", this.replyContent )
           .then((response)  =>  {
               //this.boardList = response.data.replyList;
               //this.loading = false;
               //this.linkMsg = response.data.testValue;
               this.$notifications.notify(
                {
                   component: notification,
                   horizontalAlign: 'bottom',
                   verticalAlign: 'right',
                   type: 'success'
                 })
               this.replyData(this.bno);
           }, (error)  =>  {
              this.$notifications.notify(
                {
                   component: notificationfalse,
                   horizontalAlign: 'bottom',
                   verticalAlign: 'right',
                   type: 'danger'
                 })
               this.loading = false;
           })
       },
       replyGroup : function(replyGroup){
        //  this.replys.splice (index + 1, 0, {} );
        alert("그룹번호 : "+replyGroup);
       },
       removeRow: function(index){
         this.replys.splice(index,1);
       }
       
    }
  }
</script>
<style>

</style>