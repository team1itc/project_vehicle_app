
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
          แก้ไขข้อมูลแผนก
          <v-spacer></v-spacer>
          <v-btn
            color="green lighten-2"
            flat
            @click="isEditing = !isEditing"
          >
            <i v-if="isEditing" class="fas fa-times fa-2x"></i>
            <i v-else class="fas fa-edit fa-2x "></i>
          </v-btn>
          <v-dialog v-model="conf_del" persistent max-width="290">
            <v-btn slot="activator" flat color="red lighten-2"><i class="fas fa-trash-alt fa-2x"></i></v-btn>
            <v-card>
              <v-card-title class="headline">ยืนยันการลบข้อมูล</v-card-title>
              <v-card-text>ต้องการลบข้อมูล {{d_name}}<br> ใช่หรือไม่?</v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="red lighten-2" flat @click.native="conf_del = false">ไม่ใช่</v-btn>
                <v-btn color="primary" flat @click="dep_del()">ใช่</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-card-title>
        <v-container grid-list-sm class="pa-4">
          <v-layout row wrap>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  :disabled="!isEditing"
                  :rules="[rules.required]"
                  maxlength="10"
                  counter
                  prepend-icon="fas fa-credit-card"
                  placeholder="รหัสแผนก"
                  name="d_code"
                  v-model="d_code"
                ></v-text-field>
              </v-layout>
            </v-flex>
            <v-flex xs12 >
              <v-layout align-center>
                <v-text-field
                  :disabled="!isEditing"
                  :rules="[rules.required]"
                  prepend-icon="fas fa-place-of-worship"
                  placeholder="ชื่อแผนก"
                  name="d_name"
                  v-model="d_name"
                ></v-text-field>
              </v-layout>
            </v-flex>
           
          </v-layout>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
           <v-btn flat color="red lighten-2" @click="department()">ย้อนกลับ</v-btn>
          <v-btn flat color="primary" :disabled="!isEditing" @click="dep_update(d_id)">บันทึก</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    export default {
        layout: 'manage',
        data(){
          return{
            d_code:"",
            d_name:"",
            type_api:"",
            danger:false,
            conf_del:false,
            isEditing:null,
            rules: {
                  required: value => !!value || 'ห้ามว่าง.',
                  // counter: value => value.length <= 10 || 'เต็ม 10 ตัวอักษร',
            },
          }
        },
        async created(){
          this.sh_dep()
        },
        methods:{
          conf_del(){this.conf_del=true},
          async dep_del(){//console.log("dep_del")
            let res=await this.$http.get('/department/dep_del/'+this.$route.query.d_id)
            if(res.data.ok==true){this.$router.push({name:"manage-department"})}
            else{this.danger=true,this.alt_txt=res.data.txt,this.type_api=res.data.alt}
          },
          async sh_dep(){
            let res=await this.$http.get('/department/sh_dep/'+this.$route.query.d_id)
            this.d_id=this.$route.query.d_id
            this.d_code=res.data.datas.d_code
            this.d_name=res.data.datas.d_name
          },
          async dep_update(d_id){
            //console.log("d_id"+d_id)
            let res=await this.$http.post("/department/dep_update",{
              d_code:this.d_code,
              d_name:this.d_name,
              d_id:d_id,
            })
            console.log(res.data)
              if(res.data.ok==true){this.danger=true,this.alt_txt=res.data.txt,this.type_api=res.data.alt}
             else{this.danger=true,this.alt_txt=res.data.txt,this.type_api=res.data.alt}
          },
          department(){
            this.$router.push({name: 'manage-department'})
          }
        }
    }
</script>