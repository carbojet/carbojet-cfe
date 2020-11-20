<template>
    <div class="bg-gray-100 p-0 subpixel-antialiased">
        <header class="px-4 py-3 shadow bg-blue-900">
            <div class="container mx-auto flex">
                <div>
                    <a herf="/">
                    <h1 class="text-2xl text-gray-100 tracking-wider font-bold leading-none">Fireworks</h1>
                    <h2 class="text-sm text-gray-300 tracking-widest font-semibold uppercase leading-none">Entertainment</h2>
                    </a>
                </div>
                <div class="flex w-full ml-4">
                    <!-- adding component with condition-->
                    <component :is="dynamicComponent" v-on:query-text="searchQuery"></component>
                </div>
            </div>
        </header>
    </div>
</template>
<script>
import SearchForm from './SearchForm';
export default {
    name : 'Header', 
    components:{
        SearchForm,
    },
    computed:{
        dynamicComponent(){
            if(this.$route.path!=='/'){                
                return 'SearchForm';
            }
        }
    },
    methods:{
        searchQuery(queryText){
            return queryText;
        }
    },
}
</script>