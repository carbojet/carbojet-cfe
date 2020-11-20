<template>
  <div class="container mx-auto">
      <section
        class="hero h-64 px-6 text-gray-100 flex flex-col justify-center bg-no-repeat"
        :style="'background-image: url('+bannerImg+');background-size: cover;'">
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
          <CardListBox v-for="MovieCard in MovieCards" :key="MovieCard.id" :MovieCard="MovieCard" />
        </div>
      </section>
    </div>
</template>

<script>
import CardListBox from '../components/CardListBox';
import SearchForm from '../components/SearchForm';
import backgroundUrl from '~/assets/images/hero.jpg';
import axios from 'axios';
export default {
  components : {
    CardListBox,
    SearchForm,
  },
  data(){
    return{
      bannerImg : backgroundUrl,
      MovieCards : []
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
      const res = await axios.get('https://carbojet-fe-backend.herokuapp.com/list',config);
      this.MovieCards = res.data.results;
      //console.log(res.data)
    }catch(e){
      console.log(e)
    }    
  },
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
    },
}
</script>