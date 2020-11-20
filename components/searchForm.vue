<template>    
    <form @submit.prevent="onSearchFormSubmit" class="flex w-full" style="color:#333333;">
    <input
    class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded-lg py-2 px-4 block w-full appearance-none leading-normal"
    type="text"
    placeholder="Movie or TV Series"
    v-model="queryText"
    />
    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 ml-2 rounded-lg" >Search</button>
    </form>        
</template>
<script>
import axios from "axios";
import { EventBus } from "../plugins/event-bus.js";
export default {
    name: 'SearchForm',
    components:{
        EventBus,
    },
    data(){
      return {
          queryText :'',
          searchquery:'',
          results:[]
      }        
    },
    methods : {
        async onSearchFormSubmit(){
            if(this.$route.path==='/'){
                this.$router.push({name :'results',params:{queryText:this.queryText} }) 
            }else if(this.$route.path==='/results'){            
                 EventBus.$emit("clicked-event", this.queryText)
            }else{
                this.$router.push({name :'results',params:{queryText:this.queryText} })
            }
        }        
    }
}
</script>