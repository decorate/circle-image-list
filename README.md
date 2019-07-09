
## npm-package-base

### Installation

With npm:

    npm i @team-decorate/circle-image-list
    
### Command Examples

Please inherit class ImageUploadable

```html
<circle-image-list
          :images="list"
          :interval="interval"
          active-color="red"
          :size="size"
      ></circle-image-list>
      
      
<script>
    import CircleImageList from './components/CircleImageList'
    import  {ImageUploadable} from '@team-decorate/alcjs'

    export default {
        data() {
            return {
                list: [new ImageUploadable(), {path: '/image/usericon2.jpg'}],
                interval: 10,
                size: '50'
            }
        },
        components: {
            CircleImageList
        }
    }

</script>

``` 

### props

|name|default|type|required|description|
|:---|:---|:---|:---|:---|
|images|null|Array|true|表示する画像の配列|
|interval|15|Number|---|表示する画像の間隔|
|active-color|red|String|---||
|size|'60'|String|---|画像の大きさ|

### Get active image

```html
<circle-image-list
        @clickImage="activeImage"
        :images="user.images"
></circle-image-list>


methods: {
    activeImage(index, image){
        console.log(index)
        console.log(image)
    }
}
```


