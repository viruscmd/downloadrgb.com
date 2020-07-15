<template>
    <section :style="rgb" style="height: 100vh;overflow-y: scroll;">
        <nav class="navbar header has-shadow is-transparent"
             role="navigation"
             aria-label="main navigation"
             style='background: transparent; box-shadow: none'
        >

            <div class="navbar-brand">
                <a
                        class="navbar-item"
                        href="/"
                        :style="rgb"
                >
                    Download RGB
                </a>

                <div class="navbar-burger">
                    <span/>
                    <span/>
                    <span/>
                </div>
            </div>
        </nav>

        <div class="container" style='display: grid; place-items: center;'>
            <div class="is-size-4 has-text-centered" style="height: 150px; display: grid; place-items: center">
                rgb({{red}},{{green}},{{blue}})
            </div>

            <b-field label="Red">
                <b-slider size="is-large" :min="0" :max="255" type="is-danger" v-model="red" :lazy="isLazy"></b-slider>
            </b-field>

            <b-field label="Green">
                <b-slider size="is-large" :min="0" :max="255" type="is-success" v-model="green" :lazy="isLazy"></b-slider>
            </b-field>

            <b-field label="Blue">
                <b-slider size="is-large" :min="0" :max="255" type="is-info" v-model="blue" :lazy="isLazy"></b-slider>
            </b-field>

            <b-field label="Lazy update colors">
                <b-switch v-model="isLazy"></b-switch>
            </b-field>
        </div>

    </section>
</template>

<script>

    export default {
        name: 'HomePage',
        data() {
            return {
                red: 21,
                green: 123,
                blue: 234,
                isLazy: true,
            }
        },
        computed: {
            rgb() {
                return {
                    background: `rgb(${this.red},${this.green},${this.blue})`,
                    color: `${invertColor(this.red, this.green, this.blue)} !important`,
                }
            }
        },
        mounted() {
            this.red = randomInt255();
            this.green = randomInt255();
            this.blue = randomInt255();
        }
    }


    function invertColor(r, g, b) {
        var r = parseInt(r),
            g = parseInt(g),
            b = parseInt(b);
        // http://stackoverflow.com/a/3943023/112731
        return (r * 0.299 + g * 0.587 + b * 0.114) > 186 ? '#000000' : '#FFFFFF';


    }

    function randomInt255() {
        return Math.floor(Math.random() * 256)
    }
</script>

<style>
    .field {
        width: 100%;
    }

    .container {
        padding: 0 1.5rem;
    }

    .b-slider-track {
        border: 1px solid white !important;
    }

    .label {
        color: inherit;
    }
</style>