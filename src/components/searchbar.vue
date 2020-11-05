<template>
  <v-container class="d-flex justify-center">
    <v-col  cols="8" class="text-center">
       <v-card
            class="mx-auto"
          
            outlined
        >
            <v-list-item three-line>
             
            <v-list-item-content>
                <div class="overline mb-4">
                       <h3>Nzila-l3D</h3>
                     <label for="">Get the direct link for your files</label>
                </div>
                <v-list-item-title class="headline mb-1">
                <v-text-field
                        v-model="link"
                        solo
                        label=" Past here your link..."
                        @change="error=false"
                        @keydown="error=false"
                        
                        dense
                        color="grey"
                        append-icon="mdi-link-plus"
                        @click:append="add()"
                    ></v-text-field>
                </v-list-item-title>
                <v-list-item-subtitle>
                <v-alert
                v-model="error"
                border="top"
                    color="red lighten-2"
                    dark
                dense
                    
                >
                {{msg}}
                </v-alert>
                <v-col class="pa-0 ma-0">
                    <v-list-item-group>
                        <v-list-item @click="copyToClipboard(lk)"  v-for="lk in links" :key="lk"> <v-icon>mdi-link</v-icon> {{lk}} <v-spacer></v-spacer> <v-btn  small color="primary" @click="remove(lk)"><v-icon>mdi-trash-can-outline</v-icon></v-btn></v-list-item>
                    </v-list-item-group>
                </v-col>
                </v-list-item-subtitle>
            </v-list-item-content>

        
            </v-list-item>

            <v-card-actions>
           
            </v-card-actions>
        </v-card>
    </v-col>


     <v-bottom-sheet v-model="sheet">
      <v-sheet
        class="text-center"
        height="200px"
      >
        <v-btn
          class="mt-6"
          text
          color="red"
          @click="sheet = !sheet"
        >
          close
        </v-btn>
        <div class="py-3">
         Thank you for using Nzila-L3D.
Consider sharing this link with your friends
        </div>
        <v-btn flat  color="primary" >
           
            THis tool was made by LUK3D 
        </v-btn>
      </v-sheet>
    </v-bottom-sheet>
  </v-container>
</template>

<script>
export default {
  name: "Searchbar",
    
    data(){
        return{
            links:[],
            link:null,
            error:false,
            msg:"You have allready added this link",
            sheet:false,
        }
    },
    methods:{
        add:function(){
             if(this.link == "" || this.link == null){
                 this.error = true
                 this.msg = "The link field is empty. please fill it!"

                 return
             }
             if(!this.link.split('/').includes("view?usp=sharing") || !this.link.split('/').includes("file")){
                 this.error = true
                 this.msg = "This doesn't look like a google drive link!"

                 return
             }
               let oldLink = this.link.substr(0,this.link.lastIndexOf("/")).replace("file/d/","uc?export=download&id=");
            if(this.links.includes(oldLink,0)){

                this.msg = "You have allready added this link"
                this.error = true

                console.log( this.links.indexOf(this.link))
                return null;
            }
              
                  
                    this.links.push(oldLink);
               
           

         

           

        },
        remove:function(lk){
           
         
            var filteredAry = this.links.filter(e => e !== lk)
            this.links = filteredAry
            
        },
        copyToClipboard:function(text) {
         /*    window.prompt("Copy to clipboard: Ctrl+C, Enter", text); */

            const el = document.createElement('textarea');
            el.value = text;
            el.setAttribute('readonly', '');
            el.style.position = 'absolute';
            el.style.left = '-9999px';
            document.body.appendChild(el);
            el.select();
            document.execCommand('copy');
            document.body.removeChild(el);
            this.sheet = true
        }
    }
};
</script>
