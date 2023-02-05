<template>
  <div class="comment">
    <div class="comment-info">
      <span class="comment-name">
        {{ comment.title }}
      </span>
      <span class="comment-date">
        {{ comment.date }}
      </span>
    </div>
    <div class="comment-description">
      {{ comment.decscription }}
    </div>
  </div>

</template>

<script>
export default {
  name: "comment",
  props: {
    comment: {
      type: Object,
    },
  },
}
</script>