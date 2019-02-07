<template>
  <div>
      <nav-bar></nav-bar>
  
      <div class="container-fluid" id="api-body">
        
        <div class="row">
          
          <side-bar :folder-details="folderDetails"></side-bar>
          <content-area></content-area>
          <example-area></example-area>
        
        </div>

      </div>
  </div>
</template>

<script>
import SideBar from './components/SideBar';
import navBar from './components/navBar';
import contentArea from './components/contentArea';
import exampleArea from './components/exampleArea';
import collections from '../collection.json';

export default {
  name: 'App',
  components: {
    SideBar,
    navBar,
    contentArea,
    exampleArea
  },
  data : function(){
    return {
      apiData : collections
    }
  },
  computed : {
    folderDetails (){
      var temp = {};
    
      temp['folder_order'] = this.apiData['folders_order'];
      temp['folders'] = this.apiData['folders'];
      temp['requests'] = this.apiData['requests'];
      console.log(temp);  
      return temp;

    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
