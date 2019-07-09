<template>
    <div class="circle-image-list" :style='styles'>
        <div class="inner scroll">
            <ul class="image-list">
                <li class="image-list__item"
                    @click="changeActive(image, i)"
                    v-for="(image, i) in images"
                    :class="[{'active': image.active}]">

                    <img :src="image.path"/>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import  ImageUploadable from '../models/Parents/ImageUploadable'
    import linq from 'linq'

    export default {
        name: 'circle-image-list',

        data() {
            return {
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
                type: String,
                required:false
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
                linq.from(this.images).select(x => {
                    if(x instanceof ImageUploadable){
                        return x
                    }
                    const i = new ImageUploadable()
                    i.data = x
                    return i
                })
                    .select((x,i) => {
                        if(i === 0) {
                            x.active = true
                        } else {
                            x.active = false
                        }
                        return x
                    })
                    .select((x, i) => this.images[i] = x)
                    .toArray()

            },

            changeActive(image, index) {
                linq.from(this.images)
                    .select((x, i) => {
                        x.active = false
                        return {value: x, key: i}
                    })
                    .where(x => index === x.key)
                    .forEach(x => {
                        x.value.active = true
                        this.$set(this.images, x.key, x.value)
                    })
                this.$emit('clickImage', index, image);
            }
        }
    }
</script>

<style lang="scss">
</style>

