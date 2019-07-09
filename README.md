
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
