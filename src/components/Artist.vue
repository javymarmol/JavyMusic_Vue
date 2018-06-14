<template>
    <li class="artist">
        <h2>
            <a :href="artist.url" target="_blank">{{ artist.name }}</a>
        </h2>
        <img :src="artist.image[3]['#text']" alt="">
    </li>
</template>
<script>
export default {
    name: 'artist',
    props: ['artist']
}
</script>
<style scoped>
li.artist {
  display: inline-block;
  margin: 10px 20px;
  border: #41b883 solid 2px;
  border-radius: 5px;
  padding: 5px;
  margin: 10px;
}
</style>


