<template>
    <div class="bg-gray-100 p-0 subpixel-antialiased">
        <header class="px-4 py-3 shadow bg-blue-900">
            <div class="container mx-auto flex">
                <div>
                    <h1 class="text-2xl text-gray-100 tracking-wider font-bold leading-none"><a herf="/">Fireworks</a></h1>
                    <h2 class="text-sm text-gray-300 tracking-widest font-semibold uppercase leading-none"><a herf="/">Entertainment</a></h2>
                </div>            
                <div class="flex w-full ml-4">
                    <component :is="dynamicComponent"></component>
                </div>
            </div>
        </header>
    </div>
</template>
<script>
import SearchForm from './searchForm';
export default {
    name : 'DefaultAppHeader',
    data(){
        return{
        searchResult:[],
        querytext:'working'
      }
    },
    components : {
    SearchForm
    },
    computed:{
        dynamicComponent(){
            if(this.$route.path!=='/'){                
                return 'SearchForm';
            }
        }
    },    
    methods : {
      /*
      async searchText(text){
          const config = {
            headers : {
              'Accept' : 'application/json',
            }
          }
          try{
            const res = await axios.get('https://fwemoviedb.herokuapp.com/3/search/movie?api_key=e800e93ef4806616964242bbd2619ae1&query'+this.text,config);
            this.searchResult = res.data.results;
            //console.log(res.data)
          }catch(e){
            console.log(e)
          }
      }
      */      
    }
    
}
</script>