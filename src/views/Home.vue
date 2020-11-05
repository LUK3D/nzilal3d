<template>
  <div class="home">
    <Searchbar></Searchbar>
  <Tutorial></Tutorial>
     <v-footer app>
    
    <label for="">All rights reserved to luk3d {{date()}}</label>
  </v-footer>
  </div>
  
</template>

<script>
// @ is an alias to /src
import Searchbar from '@/components/searchbar.vue'
import Tutorial from '@/components/tutorial.vue'

export default {
  name: "Home",
  components: {
    Searchbar,
    Tutorial
  },
  methods:{
     date:()=>{
        var today = new Date();
        var dd = String(today.getDate()).padStart(2, '0');
        var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
        var yyyy = today.getFullYear();

        today = mm + '/' + dd + '/' + yyyy;
        return (yyyy);  
      }
  }
};
</script>
