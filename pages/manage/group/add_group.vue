
<template>
    <v-card>
        <v-card-title
          class="grey lighten-4 py-4 title"
        >
          เพิ่มข้อมูลกลุ่ม
        </v-card-title>
        <v-container grid-list-sm class="pa-4">
          <v-layout row wrap>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  prepend-icon="fas fa-credit-card"
                  placeholder="รหัสกลุ่ม"
                  name="group_code"
                ></v-text-field>
              </v-layout>
            </v-flex>
            <v-flex xs12>
              <v-select
                :items="grp"
                v-model="group"
                menu-props="auto"
                hide-details
                label="กลุ่ม"
                prepend-icon="fas fa-users"
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
            group: '',
            gender:'',
            pre_name:"",
            grp:[
              'A1', 'A2', 'B1','B2' ,'C1','C2',"D1",'D5','E1','E5'
            ],

          }
          
        
        },
        group(){
          this.$router.push({name: 'manage-group'})
        }
    }
</script>