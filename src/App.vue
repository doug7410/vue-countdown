<template>
    <div id="app" :style="{backgroundImage: `url('/img/${this.image}')`}">
        <div>
            <h3>New Zealand - 09/29/2018</h3>
        </div>
        <div class="clock-container">
            <clock date="2018-09-29"></clock>
        </div>
    </div>
</template>

<script>
    import Clock from './components/Clock.vue'

    export default {
        name: 'app',
        data() {
            return {
                image: 'new-zealand-2.jpg',
                images: [
                    'new-zealand-2.jpg',
                    'new-zealand-3.jpg',
                    'new-zealand-4.jpg',
                    'new-zealand-5.jpg',
                    'new-zealand-6.jpg',
                    'new-zealand-8.jpg',
                    'new-zealand-9.jpg',
                    'new-zealand-10.jpg',
                    'new-zealand-11.jpg',
                    'new-zealand-12.jpg',
                ]
            }
        },
        created() {
            setInterval(() => {
                this.setImage()
            }, 12000)
        },
        components: {
            Clock
        },
        methods: {
            setImage() {
                const currentImageIndex = this.images.indexOf(this.image);
                const lastImageIndex = this.images.length - 1;

                if(currentImageIndex === lastImageIndex) {
                    this.image = this.images[0]
                } else {
                    this.image = this.images[currentImageIndex+1]
                }
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
        /*background-image: url("assets/new-zealand-3.jpg");*/
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
</style>
