<template>    
    <ListDetail :LDetail = "LDetail" />
</template>

<script>
import ListDetail from '../../../components/listDetail';
import axios from "axios";
export default {

    data(){
      return{
        LDetail:{}
      }
    },
    async created(){
      const config = {
        headers : {
          'Accept' : 'application/json',
        }
      }
      try{
        const res = await axios.get('https://fwemoviedb.herokuapp.com/3/movie/'+this.$route.params.id+'?api_key=e800e93ef4806616964242bbd2619ae1',config);
        this.LDetail = res.data;
        console.log(res.data)
      }catch(e){
        console.log(e)
      }
      
    },
    /*index Header */
    head(){
        return {
            title : this.LDetail.title,
            meta:[
                {
                    hid:"description",
                    name:"description",
                    content:"Fireworks Entertainment Latest Movies Here",
                }
            ]
        }
    },
    /* popular list component */
    components : {
      ListDetail
    }
}
</script>
