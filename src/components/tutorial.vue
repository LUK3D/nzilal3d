<template>
  <v-container class="d-flex justify-center">
    
    <v-col  cols="8" class="text-center">
         <v-btn flat small color="primary" @click="help =!help">How copy the link from Google Drive?</v-btn>
        <v-col cols="12" v-if="help">
        
    
      <div v-for="img in images" :key="img.src" class="mb-2">
          <h3>{{img.title}}</h3>
            <v-img 
            lazy-src="https://picsum.photos/id/11/10/6"
            max-height="150"
        
            :src="`${img.src}`"
            ></v-img>
            <v-divider></v-divider>
      </div>
        </v-col>
    </v-col>
  </v-container>
</template>

<script>
export default {
  name: "Tutorial",
  data(){
      return{
          images:[
             {title:"Step 01", src: "../img/steps/Web 1920 – 1.png"},
             {title:"Step 02", src: "../img/steps/Web 1920 – 2.png"},
             {title:"Step 03", src: "../img/steps/Web 1920 – 3.png"},
             
          ],
          help:false
      }
  }
  
};
</script>
