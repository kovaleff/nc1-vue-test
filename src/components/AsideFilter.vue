<template>
  <div class="filter">
    <div class="input-block">
      <label>Name:</label>
      <el-input placeholder="Name to filter" v-model="name" :disabled="!name_checked"></el-input>
      <el-switch v-model="name_checked" @change="alert('!')"></el-switch>
    </div>
    <div class="input-block">
      <label>Bedrooms</label>
      <el-input-number v-model="bedrooms" :min="1" :max="7" :disabled="!bedrooms_checked"></el-input-number>
      <el-switch v-model="bedrooms_checked"></el-switch>
    </div>
    <div class="input-block">
      <label>Bathrooms</label>
      <el-input-number v-model="bathrooms" :min="1" :max="3" :disabled="!bathrooms_checked"></el-input-number>
      <el-switch v-model="bathrooms_checked"></el-switch>
    </div>
    <div class="input-block">
      <label>Storeys</label>
      <el-input-number v-model="storeys" :min="1" :max="3" :disabled="!storeys_checked"></el-input-number>
      <el-switch v-model="storeys_checked"></el-switch>
    </div>
    <div class="input-block">
      <label>Garages</label>
      <el-input-number v-model="garages" :min="1" :max="3" :disabled="!garages_checked"></el-input-number>
      <el-switch v-model="garages_checked"></el-switch>
    </div>

    <div class="input-block">
      <label>Prices in $K</label>
      <el-slider
          v-model="prices"
          range
          show-stops
          :min="50"
          :max="500">
      </el-slider>
    </div>

    <el-button type="primary" @click="filterHandle">Apply</el-button>
  </div>
</template>

<script>
export default {
  name: 'AsideFilter',
  props: {},
  data() {
    return {
      name: '',
      bedrooms: 1,
      bathrooms: 1,
      storeys: 1,
      garages: 1,
      prices: [50, 500],

      name_checked: false,
      bedrooms_checked: false,
      bathrooms_checked: false,
      storeys_checked: false,
      garages_checked: false,
    }
  },
  methods: {
    filterHandle() {
      let checked = {};
      for (let [key, value] of Object.entries(this.$data)) {
        if (this.$data[key] && this.$data[`${key}_checked`]) {
          checked[key] = value;
        }
      }
      checked['price'] = this.$data.prices[0] + '-' + this.$data.prices[1];
      this.$emit('filtered', checked)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.filter {
  padding: 1rem;
}

.el-button--primary {
  margin: 1rem auto;
}

.input-block {
  margin: 1rem auto;
}

.input-block label {
  font-weight: bold;
}

</style>
