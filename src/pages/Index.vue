<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL+$page.posts.edges[4].node.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>全职高手</h1>
              <span class="subheading">荣耀，不是一个人的游戏</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div>
        <h2>全明星秀</h2>
      </div>
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'/post/'+edge.node.id">
              <img :src="GRIDSOME_API_URL+edge.node.cover.url" alt="" class="src" width="100%" height="700px" name="referrer" content="no-referrer"/>
              <h2 class="post-title" style="text-align:center;">{{edge.node.title}}</h2>
            </g-link>
            <!-- <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="'/tag/'+tag.id">{{tag.title}}</g-link>&nbsp;&nbsp;
              </span>
            </p> -->
            <hr />
          </div>
          <Pager :info="$page.posts.pageInfo"/>
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query ($page: Int) {
  posts: allStrapiPost (perPage: 10, page: $page) @paginate {
    pageInfo {
      totalPages,
      currentPage
    }
    edges {
      node {
        id,
        title,
        tags {
          id,
          title
        },
        cover {
          url
        }
        created_at
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'
export default {
  name: 'homepage',
  metaInfo: {
    title: "Hello, world!"
  },
  components: {
    Pager
  }
};
</script>

<style>
</style>
