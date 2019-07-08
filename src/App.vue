<template>
  <div id="app">
      <circle-image-list
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
                list: [new ImageUploadable(), new ImageUploadable(), {path: '/image/usericon2.jpg'}],
                interval: 10,
                size: '50'
            }
        },
        components: {
            CircleImageList
        }
    }

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
