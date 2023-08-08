<template>
  <el-container class="dashboard">
    <el-aside width="250px">
      <aside-filter @filtered="$emit('filtered', $event)"></aside-filter>
    </el-aside>
    <el-main>
      <el-table v-if="tableData.length"

          :data="tableData"
          border
          style="width: 100%">

        <el-table-column
            prop="name"
            label="Name"
            width="180">
        </el-table-column>
        <el-table-column
            prop="bedrooms"
            label="Bedrooms"
            width="180">
        </el-table-column>
        <el-table-column
            prop="bathrooms"
            label="Bathrooms">
        </el-table-column>
        <el-table-column
            prop="storeys"
            label="Storeys">
        </el-table-column>
        <el-table-column
            prop="garages"
            label="Garages">
        </el-table-column>
        <el-table-column
            prop="price"
            label="Price">
        </el-table-column>
      </el-table>
      <h1 v-else>There are no items (</h1>
    </el-main>
  </el-container>
</template>

<script>
import AsideFilter from './AsideFilter.vue'

export default {
  name: 'MainDashboard',
  props: ['houses'],
  components: {
    AsideFilter
  },
  data(){
    return {
    }
  },
  computed:{
    tableData() {
      return this.houses;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
