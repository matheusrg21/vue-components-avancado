<template>
  <div>
    <h2>Lista de posts</h2>
    <PostListItem 
      v-for="post in posts"
      :key="post.id"
      :post="post">
        <slot :meuPost="post"></slot>
    </PostListItem>
  </div>
</template>

<script>
import PostListItem from "./PostListItem.vue";
export default {
  components: {
    PostListItem
  },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>