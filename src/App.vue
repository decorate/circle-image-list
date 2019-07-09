<template>
  <div id="app">
      <circle-image-list
          @clickImage="activeIndex"
          :images="list"
          :interval="interval"
          active-color="blue"
          :size="size"
      ></circle-image-list>
  </div>
</template>

<script>
    import CircleImageList from './components/CircleImageList'
    import  ImageUploadable from './models/Parents/ImageUploadable'
    import 'bootstrap/dist/css/bootstrap.css'

    export default {
        data() {
            return {
                list: [new ImageUploadable()],
                interval: 10,
                size: '50',
                activeImg: null
            }
        },
        methods: {
            activeIndex(index, image) {
                console.log(index)
                console.log(image)
            }
        },
        components: {
            CircleImageList
        }
    }

</script>

<style lang="scss">
    @import './sass/style.scss';
</style>
