
<template>
    <v-card>
        <v-card-title
          class="grey lighten-4 py-4 title"
        >
          เพิ่มข้อมูลยานพาหนะ
        </v-card-title>
        <v-container grid-list-sm class="pa-4">
          <v-layout row wrap>
            <v-flex xs12 >
                <v-autocomplete
                  :loading="loading"
                  :items="item_mc_owner"
                  :search-input.sync="mc_owner_sysn"
                  v-model="mc_owner"
                  cache-items
                  class="mx-3"
                  flat
                  hide-no-data
                  hide-details
                  label="เจ้าของพาหนะ"
                ></v-autocomplete>
            </v-flex>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  prepend-icon="fas fa-id-card-alt fa-2x"
                  placeholder="ทะเบียนรถ"
                  name="std_code"
                ></v-text-field>
              </v-layout>
            </v-flex>
            <v-flex xs6 >
                <v-autocomplete
                  :loading="loading"
                  :items="item_mc_brand"
                  :search-input.sync="mc_brand_sysn"
                  v-model="mc_brand"
                  cache-items
                  class="mx-12"
                  flat
                  hide-no-data
                  hide-details
                  label="แบรนด์"
                  prepend-icon="fas fa-car"
                ></v-autocomplete>
            </v-flex>
           <v-flex xs6>
              <v-select
                :items="item_mc_series"
                v-model="mc_series"
                menu-props="auto"
                label="รุ่น"
                hide-details
                prepend-icon=""
                ></v-select>
            </v-flex>
  
          </v-layout>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn flat color="red lighten-2" >ยกเลิก</v-btn>
          <v-btn flat color="primary" >บันทึก</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    export default {
        layout: 'manage',

        data () {
            return {
              loading: false,
              mc_brand: '',
              mc_series:'',
              pre_name:"",
              item_mc_brand:['honda', 'yamaha',],
              item_mc_series:['wave 110i','jupiter 110'],
              loading: false,

              mc_owner_item: [],
              mc_owner_sysn: null,
              mc_owner: null,
              item_mc_owner: [
                'Alabama',
                'Alaska',
                'American Samoa',
                'Arizona',
                'Arkansas',
                'California',
                'Colorado',
                'Connecticut',
                'Delaware',
                'District of Columbia',
                'Federated item_mc_owner of Micronesia',
                'Florida',
              ]
            }
        },
        watch: {
          mc_owner_sysn (val) {
            val && val !== this.select && this.querySelections(val)
          },
          mc_brand_sysn (val) {
            val && val !== this.select && this.querySelections(val)
          },
          mc_series_sysn (val) {
            val && val !== this.select && this.querySelections(val)
          },

        },
        methods: {
          querySelections (v) {
            this.loading = true
            // Simulated ajax query
            setTimeout(() => {
              this.items= this.item_mc_owner.filter(e => {
                return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
              }),
              this.items = this.item_mc_brand.filter(e => {
                return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
              }),
              this.items = this.item_mc_series.filter(e => {
                return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
              }),
              this.loading = false
            }, 500)
   
          }
          
        
        }
    }
</script>