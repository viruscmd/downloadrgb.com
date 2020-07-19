<template>
    <section :style="rgbStyle" style="height: 100vh;overflow-y: scroll;">
        <nav class="navbar header has-shadow is-transparent hast-text-centered"
             role="navigation"
             aria-label="main navigation"
             style='background: transparent; box-shadow: none;border-bottom: 1px solid rgba(255,255,255,0.25)'
        >

            <div class="navbar-item">
                <a
                        class="navbar-item title has-text-centered"
                        href="/"
                        :style="rgbStyle"
                >
                    Download RGB
                </a>
            </div>
        </nav>

        <div class="container" style='display: grid; place-items: center;'>
            <div class="is-size-3 has-text-centered" style="height: 150px; display: grid; place-items: center">

                <b-tooltip label="click to copy">
                    <span @click.stop.prevent="copyColor">{{rgbValue}}</span>
                </b-tooltip>
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

        <input type="hidden" :value="rgbValue" id="copyThis">

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
                isLazy: false,
            }
        },
        computed: {
            rgbValue() {
                return `rgb(${this.red},${this.green},${this.blue})`
            },
            rgbStyle() {
                return {
                    background: `rgb(${this.red},${this.green},${this.blue})`,
                    color: `${invertColor(this.red, this.green, this.blue)} !important`,
                }
            }
        },
        methods: {
            copyColor () {
                let textToCopy = document.querySelector('#copyThis');
                textToCopy.setAttribute('type', 'text');
                textToCopy.select();

                try {
                    document.execCommand('copy');
                    this.$buefy.toast.open({
                        message: 'Copied',
                        type: 'is-success'
                    });
                } catch (err) {
                    this.$buefy.toast.open({
                        message: 'Oops, unable to copy!',
                        type: 'is-danger'
                    });
                }

                /* unselect the range */
                textToCopy.setAttribute('type', 'hidden');
                window.getSelection().removeAllRanges();
            },
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

    .navbar .navbar-item {
        text-align: center;
        display: block;
        width: 100%;
    }

    .navbar .navbar-item a{
        text-align: center !important;
    }
</style>