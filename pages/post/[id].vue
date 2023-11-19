<template>
    <div class="post-container">
        <h1 v-if="post.title">{{ post.title.rendered }}</h1>
        <div v-if="post.content" v-html="post.content.rendered"></div>
    </div>
</template>

<script>

export default{
    data: function(){
        return{
            id: this.$route.params.id,
            post:''
        }
    },
    created: function(){
        fetch(`https://wptavern.com/wp-json/wp/v2/posts/${this.id}?_fields=author,id,content,title,link`)
          .then(resp => resp.json())
          .then(data => this.post = data )
    }
}

</script>

<style>
img{
    max-width: 100%;
}
.post-container{
    max-width: 800px;
    margin: 0 auto;
}
</style>