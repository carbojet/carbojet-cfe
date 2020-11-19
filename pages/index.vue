<template>
    <div class="container mx-auto">
      <section
        class="hero h-64 px-6 text-gray-100 flex flex-col justify-center bg-no-repeat"
        :style="'background-image: url('+imgurl+');background-size: cover;'">
        <h3 class="text-4xl font-bold">Welcome!</h3>
        <h4 class="text-xl font-semibold">
          Worlds #1 search engine for Movie and TV Series.
        </h4>
        <div class="flex mt-10">
        <SearchForm />  
        </div>
      </section>
      <section class="mt-4">
        <h3 class="text-xl">Popular Movies & TV Series</h3>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
          <Popular v-for="popData in popularList" :key="popData.id" :popular="popData" />
        </div>
      </section>
    </div>
</template>

<script>
import Popular from '../components/popular';
import SearchForm from '../components/searchForm';
import backgroundUrl from '~/assets/hero.jpg';
import axios from "axios";
export default {
    components : {
      Popular,
      SearchForm
    },
    data(){
      return{
        popularList:[],
        imgurl:backgroundUrl,
      }
    },
    /*load action fetch popular list */
    async created(){
      const config = {
        headers : {
          'Accept' : 'application/json',
        }
      }
      try{
        const res = await axios.get('https://fwemoviedb.herokuapp.com/3/movie/popular?api_key=e800e93ef4806616964242bbd2619ae1',config);
        this.popularList = res.data.results;
        //console.log(res.data)
      }catch(e){
        console.log(e)
      }
      
    },
    methods : {
      /* Search query with title */
      /*
      async searchText(text){
          const config = {
            headers : {
              'Accept' : 'application/json',
            }
          }
          try{
            const res = await axios.get('https://fwemoviedb.herokuapp.com/3/search/movie?api_key=e800e93ef4806616964242bbd2619ae1&query'+this.searchText,config);
            this.searchResult = res.data.results;
            //console.log(res.data)
          }catch(e){
            console.log(e)
          }
      }
      
      onSearchFormSubmit(querytext){
          redirect({ name: 'results', params: { query: querytext } })
      }
      */
    },
    /*index Header */
    head(){
        return {
            title : 'Fireworks Entertainment',
            meta:[
                {
                    hid:"description",
                    name:"description",
                    content:"Fireworks Entertainment Latest Movies Here",
                }
            ]
        }
    }
    
}
</script>
