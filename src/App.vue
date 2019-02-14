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
                destination: 'New Zealand',
                date: 'Tue Sep 29 2019 19:45:00 GMT-0400 (Eastern Daylight Time)',
                image: {
                    name: 'new-zealand-2.jpg',
                    textColor: 'dark'
                },
                images: [

                    {
                        name: 'new-zealand-8.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'new-zealand-9.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'new-zealand-10.jpg',
                        textColor: 'light'
                    },
                    {
                        name: 'new-zealand-11.jpg',
                        textColor: 'dark'
                    },
                    {
                        name: 'new-zealand-12.jpg',
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
                return `http://res.cloudinary.com/dsteinberg/image/upload/c_scale,q_auto,w_1000/v1536159841/countdown/${this.image.name}`
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
