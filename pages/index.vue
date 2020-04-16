<template>
  <section class="container">
    <div>
      <div class="resultItems">
        <div v-for="item in results" :key="item.id" class="resultItem">
          <img :src="item.Item.mediumImageUrls[0].imageUrl" class="imgStyle">
          <dl class="dataStyle">
            <dt>
              <a :href="item.Item.itemUrl">
                商品名: {{ item.Item.itemName.slice(0,10) + "..." }}
              </a>
            </dt>
            <dd class="price">
              ¥{{ item.Item.itemPrice }}円
            </dd>
          </dl>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      results: []
    }
  },
  async asyncData ({ app }) {
    // 楽天商品検索API
    const baseUrl1 = ''

    // 楽天アプリID
    const appId = ''
    const keyword = '&keyword= 写真集'
    const getUrl = encodeURI(baseUrl1 + appId + keyword)

    const response = await app.$axios.$get(getUrl)
    return {
      results: response.Items
    }
  }
}
</script>

<style>
.resultItems {
  /* padding-left: 50px; */
  margin: 20px;
  display: flex;
  flex-wrap: wrap;
}

.resultItem {
  padding: 20px;
}
</style>
