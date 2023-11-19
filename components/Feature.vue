
<template>
    <h2>Feature component</h2>
    <div v-if="body" class="card">
        <h2>{{ body.name }}</h2>
        <img :src="body.image.filename" alt="">
    </div>

</template>

<script>
    export default {
        props:['body']
    }
</script>

<style>
    .card{
        margin-left: 2rem;
    }
    img{
        max-width:600px;
    }
</style>