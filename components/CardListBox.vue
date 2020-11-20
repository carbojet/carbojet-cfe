<template>
        <div class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3">
        <article class="overflow-hidden rounded-lg shadow-lg">
            <nuxt-link :to="'details/' + MovieCard.id">
            <img
                alt="Placeholder"
                class="block h-auto w-full"
                :src="'https://fwemoviedb.herokuapp.com/img/w1066_and_h600_bestv2'+ MovieCard.poster_path"
            />
            </nuxt-link>

            <header
            class="flex items-center justify-between leading-tight p-2 md:p-4"
            >
            <h1 class="text-lg">
                <nuxt-link class="no-underline hover:underline text-black" :to="'details/' + MovieCard.id">               
                {{MovieCard.title.substring(0,25)}}
                </nuxt-link>
            </h1>
            
            <p class="text-grey-darker text-sm">{{MovieCard.release_date}}</p>
            </header>
        </article>
        </div>          
</template>
<script>
export default {
    name : 'CardListBox',
    props : ["MovieCard","id"],
}
</script>