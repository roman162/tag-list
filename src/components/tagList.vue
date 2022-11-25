<template>
  <div>
    <ul
      class="tag__list"
      :style="{
        justifyContent: aligning === 'between' ? 'space-between' : 'flex-start'
      }"
      ref="tagList"
    >
      <template
        v-for="(tag, index) of visibleTags"
      >
        <li
          class="tag__element tag__item"
          :data-index="index"
          :key="'item' + index"
        >
          <v-icon
            v-if="tag.icon"
            class="tag__icon"
          >
            {{ tag.icon }}
          </v-icon>
          <span class="tag__text">
            {{ tag.text }}
          </span>
        </li>
        <li
          v-if="index < visibleTags.length - 1"
          class="tag__element tag__separator"
          :data-index="index"
          :key="'separator' + index"
        />
      </template>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    tags: {
      required: true,
      type: Array
    },
    aligning: {
      type: String,
      default: 'start'
    }
  },
  data () {
    return {
      visibleTags: null,
      lastIndex: 0,
      resizeKey: null
    }
  },
  created () {
    this.visibleTags = this.tags
  },  
  mounted () {
    this.changedTags()
    window.addEventListener('resize', this.resizeWindow)
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.resizeWindow)
  },
  updated() {
    this.$nextTick(function () {
      this.sliceArr()
    })
  },
  methods: {
    resizeWindow () {
      if (!this.resizeKey) {
        this.resizeKey = setTimeout(() => {
          this.changedTags()
          this.resizeKey = null
          console.log('resize')
        }, 0)
      }
    },
    changedTags () {
      const list = this.$refs.tagList
      let lastElement = list.lastElementChild
      if (lastElement.getBoundingClientRect().right > list.getBoundingClientRect().right - 15) {
        setTimeout(() => {
          this.sliceArr()
        }, 5)
      } else {
        setTimeout(() => {
          this.addArr()
        }, 5)
      }
    },
    addArr () {
      const list = this.$refs.tagList
      let lastElement = list.lastElementChild
      const index = +lastElement.dataset.index + 2
      this.visibleTags = this.tags.slice(0, index)
      if (list.lastElementChild.getBoundingClientRect().right > list.getBoundingClientRect().right - 15) {
        this.sliceArr()
      }
    },  
    sliceArr () {
      const list = this.$refs.tagList
      const lastElement = list.lastElementChild
      if (lastElement.getBoundingClientRect().right > list.getBoundingClientRect().right - 15) {
        const index = +lastElement.dataset.index
        this.visibleTags = this.tags.slice(0, index)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .tag__list{
    display: flex;
    justify-content: space-between;
    padding: 8px 16px;
    list-style: none;
    width: 100%;
    overflow: hidden;
    align-items: center;
  }

  .tag__element{
    margin-right: 10px;
    flex-shrink: 0;
  }

  .tag__icon{
    margin-right: 5px;
  }

  .tag__item{
    font-size: 30px;
    display: flex;
    text-align: center;
  }

  .tag__separator{
    border-radius: 50%;
    background-color: black;
    width: 8px;
    height: 8px;
    flex-shrink: 0;
  }
</style>
