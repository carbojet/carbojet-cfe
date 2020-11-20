<template>      
    <div class="container mx-auto pb-4">
        <SearchListBox v-for="slbox in results" :key="slbox.id" :SLBox="slbox" />
    </div>
</template>

<script>
import SearchListBox from '../../components/SearchListBox';
import { EventBus } from "../../plugins/event-bus.js";
import axios from "axios";

export default {
    components:{
        SearchListBox,
        EventBus,
    },
    data(){
        return {
            results:[],
        }
    },
     
    async created(){           
        EventBus.$on("clicked-event",async Count=> {    
            if(this.$route.params.queryText!==undefined){
                const config = {
                    headers : {
                    'Accept' : 'application/json',
                    }
                }
                try{
                    const res = await axios.get('https://carbojet-fe-backend.herokuapp.com/search/'+`${Count}`,config);
                    this.results = res.data.results   
                    //console.log(res.data)
                }catch(e){
                    console.log(e)
                }
            }else{
                this.$router.push('/')
            }
        }); 
        //console.log(this.$route.params.queryText)
        if(this.$route.params.queryText!==undefined){
            const config = {
                headers : {
                'Accept' : 'application/json',
                }
            }
            try{
                const res = await axios.get('https://fwemoviedb.herokuapp.com/3/search/movie?api_key=e800e93ef4806616964242bbd2619ae1&query='+this.$route.params.queryText,config);
                this.results = res.data.results   
                //console.log(res.data)
            }catch(e){
                console.log(e)
            }
        }else{
            this.$router.push('/')
        }
    },
    /*index Header */
    head(){
        return {
            title : 'Movies on " '+ this.$route.params.queryText+' "',
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
