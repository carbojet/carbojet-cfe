<template>    
    <form @submit.prevent="onSearchFormSubmit" class="flex w-full">
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
import axios from 'axios';
export default {
    name : 'SearchForm',
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
           
        }else{
          /* if it not a index page or root page*/
          if(this.$route.params.queryText!==''){
            this.searchquery = this.$route.params.queryText
          }
          if(this.queryText!==''){
            this.searchquery = this.queryText
          }
          console.log(this.searchquery)  
          const config = {
            headers : {
            'Accept' : 'application/json',
            }
          }
          try{
            const res = await axios.get('https://fwemoviedb.herokuapp.com/3/search/movie?api_key=e800e93ef4806616964242bbd2619ae1&query='+this.searchquery,config);
            this.results = res.data.results       
          }catch(e){
            console.log(e)
          }
        }

        

      }
    }
}
</script>