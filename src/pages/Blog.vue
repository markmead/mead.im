<template>
  <Layout title="Blogs">
    <div class="space-y-8">
      <template v-if="blogs">
        <CardLink
          v-for="blog in blogs"
          :blog="true"
          :key="blog.id"
          :subtitle="blog.readable_publish_date"
          :summary="blog.description"
          :title="blog.title"
          :to="blog.url"
        />
      </template>
      <div v-else class="min-h-screen"></div>
    </div>
  </Layout>
</template>

<script>
import axios from 'axios'

import CardLink from '@/components/CardLink'

export default {
  data() {
    return {
      blogs: null,
    }
  },
  async beforeMount() {
    await axios.get('https://dev.to/api/articles?username=markmead').then((res) => {
      this.blogs = res.data
    })
  },
  components: {
    CardLink,
  },
  metaInfo: {
    title: 'Development Blogs',
    meta: [
      {
        name: 'description',
        content: 'Blogs that I have written about development, featuring; tips, tutorials and more',
      },
    ],
  },
}
</script>
