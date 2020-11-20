<template>
    <div class="container mx-auto p-4 flex">
        <img
        :src="'https://fwemoviedb.herokuapp.com/img/w440_and_h660_face'+DBox.poster_path"
        :alt="DBox.title"
        class="rounded h-64 mr-4"
        />
        <div class="w-full">
            <h1 class="text-3xl">{{DBox.title}}</h1>
            <p class="text-grey-darker text-sm">{{DBox.release_date}}</p>
            <p>
            {{DBox.overview}}
            </p>
        </div>
    </div>          
</template>
<script>
export default {
    name : 'DetailBox',
    props : ["DBox","id"],
}
</script>