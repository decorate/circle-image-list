<template>
    <div class="circle-image-list" :style='styles'>
        <div class="inner scroll">
            <ul class="image-list">
                <li class="image-list__item"
                    @click="changeActive(i)"
                    v-for="(image, i) in convertData"
                    :class="[{'active': i === select}]">

                    <img :src="image.path"/>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import  ImageUploadable from '../models/Parents/ImageUploadable'
    import linq from 'linq'
    import '../sass/style.scss'
    import '../../dist/circle-image-list.css'

    export default {
        name: 'circle-image-list',

        data() {
            return {
                convertData: [],
                select: 0
            }
        },

        props: {
            images: {
                type: Array,
                required:true
            },
            size: {
                type: String,
                default: '60'
            },
            interval: {
                type: Number,
                default: 15
            },
            activeColor: {
                type: String
            }
        },

        created() {
            this.convert()
        },

        computed: {
            styles() {
                let style = {}
                if(this.size){
                    style['--width'] = this.size+'px'
                    style['--height'] = this.size+'px'
                    style['--minWidth'] = this.size+'px'
                }
                if(this.interval){
                    style['--marginRight'] = this.interval +'px'
                }
                style['--activeColor'] = this.activeColor

                return style
            }
        },

        mounted() {
        },

        methods: {
            convert() {
                this.convertData = linq.from(this.images).select(x => {
                    if(x instanceof ImageUploadable){
                        return x
                    }
                    const i = new ImageUploadable()
                    i.data = x
                    return i
                })
                    .select((x,i) => {
                        if(!i) {
                            x.active = true
                        } else {
                            x.active = false
                        }
                        return x
                    })
                    .toArray()
            },

            changeActive(index) {
                linq.from(this.convertData).forEach((x,i) => {
                    x.active = (i === index)? true : false
                })
                this.select = index
            }
        }
    }
</script>

<style lang="scss">
</style>

