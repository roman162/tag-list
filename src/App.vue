<template>
  <div id="app">
    <tag-list
      :tags="tags"
      :aligning="'start'"
      class="tag__list-container tag__list-container-1"
    />
    <tag-list
      :tags="tags"
      :aligning="'between'"
      class="tag__list-container tag__list-container-2"
    />
    <tag-list
      :tags="tags"
      :aligning="'start'"
      class="tag__list-container tag__list-container-3"
    />
    <tag-list
      :tags="tags"
      :aligning="'between'"
      class="tag__list-container tag__list-container-4"
    />
  </div>
</template>

<script>
import tagList from './components/tagList.vue'

export default {
  name: 'App',
  components: {
    tagList
  },
  data () {
    return {
      tags: [
        {
          text: 'test1'
        },
        {
          text: 'test2',
          icon: 'mdi-coffee'
        },
        {
          text: 'test3',
          icon: 'mdi-cloud-sync'
        },
        {
          text: 'test4'
        },
        {
          text: 'test5',
          icon: 'mdi-cloud-check-variant'
        },
        {
          text: 'test6',
          icon: 'mdi-circle-outline'
        },
        {
          text: 'test7',
          icon: 'mdi-chess-rook'
        },
        {
          text: 'test8',
        },
        {
          text: 'test9',
        },
        {
          text: 'test10',
        },
        {
          text: 'test11',
        },
        {
          text: 'test12',
        }
      ]
    }
  }
}
</script>

<style scoped lang="scss">
  .tag__list-container{
    margin-bottom: 16px;
  }

  .tag__list-container-1{
    width: 50vw;
  }

  .tag__list-container-2{
    width: 50vw;
  }

  .tag__list-container-3{
    width: 100vw;
  }

  .tag__list-container-4{
    width: 100vw;
  }
</style>
