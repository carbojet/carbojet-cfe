<template>    
    <div class="container mx-auto pb-4">
        <ListBox v-for="lbox in results" :key="lbox.id" :lBox="lbox" />
    </div>
</template>

<script>
import ListBox from '../../components/listBox';
import axios from "axios";

export default {
    components:{
        ListBox,
    },
    data(){
        return {
            results:[],
        }
    },
    async created(){
        console.log(this.$route.params.queryText)
        if(this.$route.params.queryText!==undefined){
            const config = {
                headers : {
                'Accept' : 'application/json',
                }
            }
            try{
                const res = await axios.get('https://fwemoviedb.herokuapp.com/3/search/movie?api_key=e800e93ef4806616964242bbd2619ae1&query='+this.$route.params.queryText,config);
                this.results = res.data.results   
                console.log(res.data)
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
            title : 'Fireworks Entertainment Results',
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
