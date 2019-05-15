<template>
  <div class="media">
    <div class="media-left">
      <figure class="image is-32x32">
        <img
          class="is-rounded"
          :src="pictureUrl"
        >
      </figure>
    </div>

    <div class="media-content">
      <div class="content">
        <span
          class="name has-text-weight-semibold has-text-white"
          v-if="from"
        >
          {{ from.name }}
        </span>

        <span class="has-text-white">{{ message }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    from: {
      type: Object
    },

    message: {
      type: String
    }
  },

  computed: {
    pictureUrl () {
      if (!this.from) {
        return null
      }

      return `https://graph.facebook.com/${this.from.id}/picture`
    }
  }
}
</script>

<style lang="scss" scoped>
.media {
  background: rgba(10, 10, 10, 0.5);
  border: none;

  padding: 0.5rem;
  margin: 0.25rem 0;

  .media-content {
    margin-top: 0.25rem;
  }
}

.name {
  margin-right: 0.5rem;
}
</style>
