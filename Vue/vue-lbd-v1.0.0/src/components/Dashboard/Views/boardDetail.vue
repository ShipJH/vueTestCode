<template>
   <card>
    <h4 slot="header" class="card-title">Detail</h4>
    <form>
      <div class="row">
        <div class="col-md-4">
          <fg-input type="text"
                    label="Title"
                    placeholder="Username"
                    :disabled="true"
                    v-model="boardDetail.title">
          </fg-input>
        </div>
      </div>

      <div class="row">
        <div class="col-md-8">
          <div class="form-group">
            <label>content</label>
            <textarea rows="5" class="form-control border-input"
                      placeholder="Here can be your description"
                      :disabled="true"
                      style="height:250px;"
                      v-model="boardDetail.content">
              </textarea>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-3">
          <fg-input type="text"
                    label="reg_date"
                    placeholder="City"
                    :disabled="true"
                    v-model="boardDetail.regDate">
          </fg-input>
        </div>
      </div>
      <div class="text-center">
        <button type="submit" class="btn btn-info btn-fill float-right" @click.prevent="updateProfile">
          Update
        </button>
      </div>
      <div class="clearfix"></div>
    </form>
  </card>
</template>

<script>
  import Card from 'src/components/UIComponents/Cards/Card.vue'

  export default {
    name: 'app1',
    props: [
    'bno'
    ],
    components: {
      Card
    },
    data: function () {
        return {
            boardDetail: [],
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