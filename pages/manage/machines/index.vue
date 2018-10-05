<template>
  <div>
    <div class="cv_header">ข้อมูลยานพาหนะ</div>
  <v-data-table
      :headers="headers"
      :items="desserts"
      :search="search"
      :pagination.sync="pagination"
      hide-actions
      class="elevation-1"
    >
    <template slot="headerCell" slot-scope="props">
      <v-tooltip bottom>
        <span slot="activator">
          {{ props.header.text }}
        </span>
        <span>
          {{ props.header.text }}
        </span>
      </v-tooltip>
    </template>
    <template slot="items" slot-scope="props" >
      <td class="text-xs-left">{{ props.item.mc_code }}</td>
      <td class="text-xs-left">{{ props.item.mc_brand }}</td>
      <td class="text-xs-left">{{ props.item.mc_serie }}</td>
    </template>
  </v-data-table>
   <div class="text-xs-center pt-2">
      <v-pagination v-model="pagination.page" :length="pages"></v-pagination>
    </div>
  </div>
</template>

<script>
  export default {
    layout: 'manage',
    data () {
      return {
        search: '',
        pagination: {},
        selected: [],
        headers: [
          { text: 'ทะเบียนรถ', value: 'ทะเบียนรถ',align: 'left',sortable: false, },
          { text: 'ยี่ห้อ', value: 'ยี่ห้อ',align: 'left',sortable: false,  },
          { text: 'รุ่น', value: 'รุ่น',align: 'left',sortable: false,  },
         
        ],
        desserts: [
          {
            value: false,
            mc_code: 'กพค 876',
            mc_brand: 'honda',
            mc_serie:'wave110',          
          },
           {
            value: false,
            mc_code: 'กพค 876',
            mc_brand: 'honda',
            mc_serie:'wave110',          
          },
           {
            value: false,
            mc_code: 'กพค 876',
            mc_brand: 'honda',
            mc_serie:'wave110',          
          },
           {
            value: false,
            mc_code: 'กพค 876',
            mc_brand: 'honda',
            mc_serie:'wave110',          
          },
           {
            value: false,
            mc_code: 'กพค 876',
            mc_brand: 'honda',
            mc_serie:'wave110',          
          },
         
        ]
      }
    },
    computed: {
      pages () {
        if (this.pagination.rowsPerPage == null || this.pagination.totalItems == null) return 0
        return Math.ceil(this.pagination.totalItems / this.pagination.rowsPerPage)
      }
    }
  }
</script>