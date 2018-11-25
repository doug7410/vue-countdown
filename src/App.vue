<template>
    <div>
        <div id="app"
             :style="{backgroundImage: `url('${this.imageUrl}')`}">
            <div class="description" :class="textColor">
                <h3>{{ destination }} - {{ tripDate }}</h3>
            </div>
            <div class="clock-container">
                <clock :date="date"/>
            </div>
        </div>
    </div>
</template>

<script>
    import Clock from './components/Clock.vue'

    export default {
        name: 'app',
        data() {
            return {
                destination: 'Angie Comes Home!!',
                date: 'Sun Nov 25 2018 10:00:00 GMT-0500 (Eastern Daylight Time)',
                image: {
                    name: 'IMG_1682.jpg',
                    textColor: 'dark'
                },
                images: [
                    {
                        name: 'IMG_1828.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_0990.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_1586.jpg',
                        textColor: 'light'
                    },
                    {
                        name: 'IMG_2259.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_1544.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_5278.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_5233.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_1363.jpg',
                        textColor: 'light'
                    },
                    {
                        name: 'IMG_1281.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'IMG_0986.jpg',
                        textColor: 'dark'
                    },
                ]
            }
        },
        created() {
            setInterval(() => {
                this.setImage()
            }, 6000)
        },
        components: {
            Clock
        },
        methods: {
            setImage() {
                const currentImageIndex = this.images.indexOf(this.image)
                const lastImageIndex = this.images.length - 1

                if (currentImageIndex === lastImageIndex) {
                    this.image = this.images[0]
                } else {
                    this.image = this.images[currentImageIndex + 1]
                }
            }
        },
        computed: {
            tripDate() {
                const date = new Date(this.date)
                return date.toLocaleDateString() + ' - ' + date.toLocaleTimeString()
            },
            imageUrl() {
                return `https://res.cloudinary.com/dsteinberg/image/upload/c_scale,q_auto,w_1000/v1543115811/dougandangie/${this.image.name}`
            },
            textColor() {
                if (this.image.textColor === 'dark') {
                    return 'text-dark'
                }

                return 'text-light'
            }
        }
    }
</script>

<style lang="scss">
    @import "./scss/main";

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        background-size: cover;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        display: flex;
        align-items: center;
        flex-direction: column;
        background-color: black;
    }

    .clock-container {
        width: 100%;
    }

    .description {
        font-size: 1.1rem;
    }

    .text-dark {
        color: #263238;
    }

    .text-light {
        color: #ffffff;
    }
</style>
