<template>
  <section class="section container">
    <div class="columns">
        <div class="column is-one-third" :style="rgb" style='display: grid; place-items: center; min-height:200px'>
          <div class="has-text-centered">
            rgb({{red}},{{green}},{{blue}})
          </div>
        </div>

      <div class="column">
        <b-field label="Red">
          <b-slider :min="0" :max="255" type="is-danger" v-model="red" :lazy="isLazy"></b-slider>
        </b-field>

        <b-field label="Green">
          <b-slider :min="0" :max="255" type="is-success" v-model="green" :lazy="isLazy"></b-slider>
        </b-field>

        <b-field label="Blue">
          <b-slider :min="0" :max="255" type="is-info" v-model="blue" :lazy="isLazy"></b-slider>
        </b-field>

        <b-field label="Lazy update colors">
          <b-switch v-model="isLazy"></b-switch>
        </b-field>
      </div>
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
          color: `${invertColor(this.red,this.green,this.blue)}`,
        }
      }
    }
  }


function invertColor(r,g,b) {
    var r = parseInt(r),
        g = parseInt(g),
        b = parseInt(b);
    // http://stackoverflow.com/a/3943023/112731
    return (r * 0.299 + g * 0.587 + b * 0.114) > 186 ? '#000000' : '#FFFFFF';
  
  
}
</script>
