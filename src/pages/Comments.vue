<template>
  <div>
    <Comment
      v-for="(comment, i) in comments"
      :key="comment.id"

      :from="comment.from"
      :message="comment.message"
    />
  </div>
</template>

<script>
import Comment from '@/components/Comment'

export default {
  components: { Comment },

  data: () => ({
    comments: [],

    eventSource: null
  }),

  computed: {
    videoId () {
      return this.$route.query.video_id
    },

    accessToken () {
      return this.$route.query.access_token
    },

    limit () {
      return this.$route.query.limit || 10
    },

    eventSourceUrl () {
      return `https://streaming-graph.facebook.com/${this.videoId}/live_comments?` +
        `fields=from{name,id},message&access_token=${this.accessToken}`
    }
  },

  created () {
    this.eventSource = new EventSource(this.eventSourceUrl)

    this.eventSource.onmessage = e => this.onComment(e)
  },

  methods: {
    onComment (e) {
      this.comments.push(JSON.parse(e.data))

      if (this.comments.length > this.limit) {
        this.comments.shift()
      }
    }
  }
}
</script>
