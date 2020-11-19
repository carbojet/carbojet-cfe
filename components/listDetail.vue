<template>
    <div class="container mx-auto p-4 flex">
        <img
        :src="'https://fwemoviedb.herokuapp.com/img/w440_and_h660_face'+LDetail.poster_path"
        :alt="LDetail.title"
        class="rounded h-64 mr-4"
        />
        <div class="w-full">
            <h1 class="text-3xl">{{LDetail.title}}</h1>
            <p class="text-grey-darker text-sm">{{LDetail.release_date}}</p>
            <p>
            {{LDetail.overview}}
            </p>
        </div>
    </div>          
</template>
<script>
export default {
    name : 'ListDetail',
    props : ["LDetail","id"],
}
</script>