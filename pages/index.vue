<template>
    <div>
        <div class="flex justify-between mx-[92px]">
            <div>
                <a href="Index.php"><img src="kweltalogo.png" class="h-[6rem] w-auto"></a>
            </div>
            <a title="Hive Blockchain" href="http://www.hive.io" target="_blank"><img src="hive.png" class="h-[3rem] w-auto powered-img"></a>
        </div>
        <div class="flex flex-wrap justify-center gap-x-4">
            <div
                v-for="article in articles"
                :key="article.url"
                class="mb-4 max-w-xl px-8 py-4 bg-white rounded-lg shadow-md dark:bg-gray-500 hover:scale-[1.025] duration-100"
                style="cursor: auto;"
            >
                <a :href="article.link" target="_blank">
                    <div class="flex justify-between align-start">
                        <div class="mt-2 mb-2">
                            <h1 class="text-base text-gray-800">{{ article.pubDate }}</h1>
                            <h2 class="text-[1.6rem] font-bold text-gray-700 dark:text-white dark:hover:text-gray-400">{{ article.title }}</h2>
                        </div>
                    </div>
                    <img :src="article.img" :alt="article.title" />
                    <p class="text-gray-100 dark:text-gray-100">{{ article.description }}</p>
                    <div class="flex align-end justify-end mt-4">
                        <a :href="article.link" target='_blank' class="text-blue-700 dark:text-blue-400 hover:font-medium">Leer más ⟶</a>
                    </div>
                </a>
            </div>
        </div>
        <div class="text">
            <p><center>hecho con ❤️ por <a href="https://twitter.com/kwelta_tech">kwelteras y kwelteros.</a></center></p>
            <p><center>KWelta.tech 2022</center></p>
        </div>
    </div>
</template>

<script>
import Parser from 'rss-parser'
export default {
  name: 'IndexPage',

  data () {
    return {
      articles: null,
      metadata: null,
      loading: true
    }
  },

  async mounted () {
    const proxy = 'https://lugodev-cors-anywhere.herokuapp.com/'
    const url = 'https://hiverss.com/@kweltatech?interface=peakd'
    const parser = new Parser()
    const blog = await parser.parseURL(proxy + url)
    try {
      const articles = blog.items
      articles.forEach((article) => {
        article.img = article.content.match(/<img[^>]+src="([^">]+)"/)[1]
      })
      this.articles = articles
    } catch (e) {
      //
    }
    console.log(this.articles)
    this.loading = false
  }
}
</script>

<style>
body{
  margin-left: 0px;
  margin-right: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}

img{
    margin-top: 40px;
    margin-left: 0px;
    margin-right: 10px;
    margin-bottom: 20px;
}

.powered-img{
    margin-top: 85px;
    margin-left: 0px;
    margin-right: 10px;
    margin-bottom: 20px;
}

.text{
    color: gray;
    margin-bottom: 20px;
}
</style>
