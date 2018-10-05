
<template>
    <v-card>
      <v-alert
        v-model="danger"
        dismissible
        :type=type_api
      >
        {{alt_txt}}
      </v-alert>
        <v-card-title
          class="grey lighten-4 py-4 title"
        >
          เพิ่มข้อมูลนักเรียน / นักศึกษา
        </v-card-title>
        <v-container grid-list-sm class="pa-4">
          <v-layout row wrap>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  prepend-icon="fas fa-id-card-alt fa-2x"
                  placeholder="รหัสประจำตัวนักเรียน / นักศึกษา"
                  name="std_code"
                  v-model="std_code"
                ></v-text-field>
              </v-layout>
            </v-flex>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  prepend-icon="fas fa-id-card fa-2x"
                  placeholder="รหัสประจำตัวประชาชน"
                  name="std_pin_id"
                  v-model="std_pin_id"
                ></v-text-field>
              </v-layout>
            </v-flex>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  prepend-icon="fas fa-th"
                  placeholder="รหัสกลุ่มการเรียน"
                  name="g_code"
                  v-model="g_code"
                ></v-text-field>
              </v-layout>
            </v-flex>
           <v-flex xs4>
              <v-select
                :items="item_pre_name"
                v-model="std_prename"
                menu-props="auto"
                label="คำนำหน้าชื่อ"
                hide-details
                prepend-icon="fas fa-user"
              
                ></v-select>
            </v-flex>
            <v-flex xs4 >
                <v-text-field
                  prepend-icon=""
                  placeholder="ชื่อ"
                  name="std_name"
                  v-model="std_name"
                ></v-text-field>
            </v-flex>
            <v-flex xs4 >
                <v-text-field
                  prepend-icon=""
                  placeholder="นามสกุล"
                  name="std_lname"
                  v-model="std_lname"
                ></v-text-field>
            </v-flex>
           <v-flex xs12>
              <v-text-field
                prepend-icon="fas fa-birthday-cake"
                placeholder="วัน เดือน ปี เกิด เช่น 8 พฤษภาคม 2540"
                name="std_birthday"
                v-model="std_birthday"
                ></v-text-field>
            </v-flex>
            
            <!-- <v-flex xs6>
              <v-select
                :items="gd"
                v-model="std_gender"
                menu-props="auto"
                hide-details
                label="เพศ"
                prepend-icon="fas fa-transgender"
              
              ></v-select>
            </v-flex> -->
            <v-flex xs6>
              <v-select
                :items="bld"
                v-model="std_blood"
                menu-props="auto"
                hide-details
                label="กรุ๊ปเลือด"
                prepend-icon="fas fa-hospital"
              
              ></v-select>
            </v-flex>
           
          </v-layout>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn flat color="red lighten-2" @click="student()">ยกเลิก</v-btn>
          <v-btn flat color="primary" @click="std_add">บันทึก</v-btn>
        </v-card-actions>
        
    </v-card>
    
</template>

<script>
    export default {
        layout: 'manage',

        data () {
            return {

            std_code:"",
            std_gender:"",
            std_prename:"",
            std_name:"",
            std_lname:"",
            std_pin_id:"",
            std_birthday:"",
            std_blood:"",
            g_code:"",
            type_api:"",
            danger:false,
            alt_txt:"",
            bld:['A', 'B', 'O','AB' ],
            // gd:[{text:'ชาย',value:"ช"},{text:'หญิง',value:"ญ"}],
            item_pre_name:['นาย','นางสาว','นาง',],

          }
          
        
        },
        watch:{
          std_prename(newValue){
            if(newValue=="นาย"){this.std_gender="ช"}else{this.std_gender="ญ"}
          },
        },
        methods:{
          async std_add(){
            let res= await this.$http.post('student/std_add',{
              std_code:this.std_code,
              std_gender:this.std_gender,
              std_prename:this.std_prename,
              std_name:this.std_name,
              std_lname:this.std_lname,
              std_pin_id:this.std_pin_id,
              std_birthday:this.std_birthday,
              std_blood:this.std_blood,
              g_code:this.g_code,
              rules: {
                required: value => !!value || 'ห้ามว่าง.',
                counter_10: value => value.length <= 10 || 'เต็ม 10 ตัวอักษร',
                counter_13: value => value.length <= 10 || 'เต็ม 10 ตัวอักษร',
              }
            })
            if(res.data.ok==true){this.danger=true,this.alt_txt=res.data.txt,this.type_api=res.data.alt}
            else{this.danger=true,this.alt_txt=res.data.txt,this.type_api=res.data.alt}
          },
          student(){
            this.$router.push({name:"manage-student"})
          }
        },

    }
</script>