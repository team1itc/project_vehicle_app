
<template>
    <v-card>
        <v-card-title
          class="grey lighten-4 py-4 title"
        >
          ตั้งค่าความปลอดภัย 
        </v-card-title>
        <v-container grid-list-sm class="pa-4">
          <v-layout row wrap>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  :append-icon="stg_password ? 'visibility' : 'visibility_off'"
                  :rules="[rules.required, rules.min]"
                  :type="stg_password ? 'text' : 'password'"
                  name="password"
                  label="Password"
                  value=""
                  v-model="password"
                  class="input-group--focused"
                  @click:append="stg_password = !stg_password"
                ></v-text-field>
              </v-layout>
            </v-flex>      
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  :append-icon="stg_password2 ? 'visibility' : 'visibility_off'"
                  :rules="[rules.required, rules.min,rules.confirm_pass]"
                  :type="stg_password2 ? 'text' : 'password'"
                  name="confirm_password"
                  label="Confirm Password"
                  value=""
                  v-model="conf_pass"
                  class="input-group--focused"
                  @click:append="stg_password2 = !stg_password2"
                ></v-text-field>
              </v-layout>
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
            std_code:"6039010001",
            pin_id:"1234567890987",
            pre_name:"",
            std_name:"นักเรียน",
            std_lname:"คนนึง",
            std_birthday:"8 พฤษภาคม 2540",
            blood: '',
            gender:'',
            bld:[
              'A', 'B', 'O','AB' 
            ],
            gd:['ชาย','หญิง'],
            item_pre_name:['นาย','นางสาว','นาง',],
            stg_password: false,
            stg_password2: false,
            password:"",
            conf_pass:"",
            rules: {
              required: value => !!value || 'ห้ามว่าง.',
              min: v => v.length >= 8 || 'Password ไม่ควรน้อยกว่า 8 ตัวอักษร',
              emailMatch: () => ('The email and password you entered don\'t match'),

            },
          }
          
          
        
        },
        
    }
</script>