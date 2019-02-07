<template>
  
    <div class="col-3" id="side-bar-body">
        <ul style="list-style-type:none;padding-inline-start:10px;">
        
          <li v-for="folderName in folderNames" :key="folderName.id" class="folder-name">
            <div class="project-list">
             
              <span class="folder-image" v-if="displayRequest == folderName.id">
                 <img  src="../assets/folder-close.svg" alt="">
              </span>

              <span class="folder-image" v-if="displayRequest == null || displayRequest != folderName.id">
                 <img  src="../assets/folder-open.svg" alt="">
              </span>
              
              <span class="project-name" :id="folderName.id" v-on:click="toggleRequestList($event)">
                {{ folderName.name }}
              </span>

            </div>

            <ul style="list-style-type:none;padding-inline-start:10px;" v-if="displayRequest == folderName.id" class="folder-request-methods">
              <li v-for="request in folderName.requests" :key="request.id" >
                
                <div class="request-lists">

                  <div class="request-method">
                    <div :class="request.methods" class="methods-name"> {{ request.methods }}  </div>
                  </div>
                  
                  <div class="request-name">
                    {{ request.name }}
                  </div>

                </div>
                
              </li>
            </ul>

          </li>
        
        </ul>   
    </div>
  
</template>

<script>
export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      folderNames : this.orderFolders(),
      displayRequest : null
    }
  },
  props : {
    folderDetails : Object
  },
  methods : {

    orderFolders (){

      var folderList = [];
      debugger;
      for(var i = 0 ; i < this.folderDetails['folder_order'].length ; i++){

        for(var y = 0 ; y < this.folderDetails['folders'].length ; y++){

          if(this.folderDetails['folder_order'][i] == this.folderDetails['folders'][y].id){

                var temp = {
                  id : this.folderDetails['folders'][y].id,
                  name : this.folderDetails['folders'][y].name,
                  requests : []
                }
            debugger;
            for(var z = 0 ; z < this.folderDetails['requests'].length ; z++){ 
              if(this.folderDetails['requests'][z]['folder'] == this.folderDetails['folders'][y].id){
               
                temp['requests'].push({
                  methods : this.folderDetails['requests'][z].method,
                  name : this.folderDetails['requests'][z].name, 
                  id : this.folderDetails['requests'][z].id, 
                })
                
              }
            }
            console.log(temp)
            folderList.push(temp);

          }

        }

      }

      return folderList;
    },
    toggleRequestList (event){
      
      if(this.displayRequest == event.currentTarget.id){
        this.displayRequest = null;
      }else{
        this.displayRequest = event.currentTarget.id;
      }
      
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#side-bar-body{
  background-color: #f5f5f5;
  height: 100%;
  padding: 20px 10px 20px 10px;
}

.project-list{
  padding: 3px 0;
  font-weight: 600 !important;
}
.project-name{
  cursor: pointer;
  letter-spacing: 0.2px;
  -webkit-user-select: none; /* webkit (safari, chrome) browsers */
    -moz-user-select: none; /* mozilla browsers */
    -khtml-user-select: none; /* webkit (konqueror) browsers */
    -ms-user-select: none; /* IE10+ */
}
.request-lists{
  font-size: 15px;
  padding: 2px 0 7px 0;
  line-height: 1;
}

.methods-name{
  font-weight: 800;
}
#folder-name{
  padding: 2px 2px 2px 2px !important;
}

.request-name{
  display:table;
}

.request-method{
  float: left;
  width: 40px;
  font-size: 12px;
  margin-right: 10px;
  line-height: 1.6;
  text-align: right;
}

.folder-image{
  /* margin-bottom: 2px;  */
}

.GET{
  color: #3eb63e;
}

.PATCH {
  color: #666;
}

.POST{
  color: #f5a623;
}

.DELETE {
  color: #ed4b48;
}
</style>
