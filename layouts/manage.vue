<template>
  <v-app id="inspire">
    <v-navigation-drawer
      :clipped="$vuetify.breakpoint.lgAndUp"
      v-model="drawer"
      fixed
      app
    >
      <v-list dense>
        <template v-for="item in items">
          <v-layout
            v-if="item.heading"
            :key="item.heading"
            row
            align-center
          >
          <v-flex xs6>
              <v-subheader v-if="item.heading">
                {{ item.heading }}
              </v-subheader>
           </v-flex>
          </v-layout>
          <v-list-group
            v-else-if="item.children"
            v-model="item.model"
            :key="item.text"
            :prepend-icon="item.model ? item.icon : item['icon-alt']"
            append-icon=""
          >
            <v-list-tile slot="activator">
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ item.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
            <v-list-tile
              v-for="(child, i) in item.children"
              :key="i"
              :to="child.link"
            >
              <v-list-tile-action v-if="child.icon" >
                <v-icon>{{ child.icon }}</v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ child.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list-group>
           <v-divider
            v-else-if="item.divider"
            :key="item.divider"
            dark
            class="my-3"
          ></v-divider>
          <v-list-tile v-else :key="item.text" :to="item.link">
            <v-list-tile-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>
                {{ item.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          
        </template>
      </v-list>
       <v-divider></v-divider>
    </v-navigation-drawer>
    <v-toolbar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      color="blue darken-3"
      dark
      app
      fixed
    >
      <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
        <v-toolbar-side-icon><i class="fas fa-motorcycle fa-2x"></i></v-toolbar-side-icon>
        <span class="hidden-sm-and-down">CTC Parking</span>
      </v-toolbar-title>
      <v-text-field
        flat
        solo-inverted
        hide-details
        prepend-inner-icon="search"
        label="ค้นหา ..."
        class="hidden-sm-and-down"
      ></v-text-field>
      <v-spacer></v-spacer>
      <v-btn icon>
      <v-badge right
        v-model="noti_sh"
        color="red darken-3"
      
      >
            <span v-if="num_noti" slot="badge">{{num_noti}}</span>
            <v-icon
              @click="noti_sh = !noti_sh"
              color="white"
            >notifications</v-icon>
          </v-badge>
      </v-btn>
      <v-divider
        class="mx-3"
        inset
        vertical
      ></v-divider>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <!--
      <v-btn icon large>
        <v-avatar size="32px" tile>
          <img
            src="https://cdn.vuetifyjs.com/images/logos/logo.svg"
            alt="Vuetify"
          >
        </v-avatar>
      </v-btn>
      -->
    </v-toolbar>
    <v-content>
      <v-container  xs12 >

            <nuxt/>
 
      </v-container>
    </v-content>
    <!--
    <v-btn
      fab
      bottom
      right
      color="#6c9e37"
      dark
      fixed
      @click="dialog = !dialog"
    >
      <v-icon>add</v-icon>
    </v-btn>
    <v-dialog v-model="dialog" width="800px">
      
    </v-dialog>
    -->
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      noti_sh:true,
      num_noti:'10',
      dialog: false,
      drawer: null,
      items: [
      { icon: 'fas fa-chalkboard', text: 'dashboard' ,link: ''},
      { divider: true },
       { heading: 'จัดการข้อมูล' },
        {
          icon: 'keyboard_arrow_up',
          'icon-alt': 'keyboard_arrow_down',
          text: 'เพิ่มข้อมูล',
          model: false,
          children: [
            { icon:'add' ,text: 'นักเรียน / นักศึกษา' ,link: '../../manage/student/add_student'},
            { icon:'add' ,text: 'ครู / บุคลากร' ,link: '../../manage/teacher/add_teacher'},
            { icon:'add' ,text: 'แผนกวิชา' ,link: '../../manage/department/dep_add'},
            { icon:'add', text: 'กลุ่มการเรียน' ,link: '../../manage/group/add_group'},
            { icon:'add' ,text: 'ยานพาหนะ' ,link: '../../manage/machines/data_add_machine'},
          ]
        },

        { icon: 'fas fa-user-graduate', text: 'นักเรียน / นักศึกษา' ,link: '../../manage/student'},
        { icon: 'fas fa-chalkboard-teacher', text: 'ครู / บุคลากร' ,link: '../../manage/teacher'},
        { icon: 'fas fa-place-of-worship', text: 'แผนกวิชา' ,link: '../../manage/department'},
        { icon: 'fas fa-users', text: 'กลุ่มการเรียน' ,link: '../../manage/group'},
        { icon: 'fas fa-motorcycle', text: 'ยานพาหนะ' ,link: '../../manage/machines'},

        { divider: true },
        { icon: 'delete', text: 'ถังขยะ' ,link: 'trash'},
        { divider: true },
        { 
         icon: 'keyboard_arrow_up',
          'icon-alt': 'settings',
          text: 'ตั้งค่า', 
         model: false,
          children: [
            { icon:'fas fa-user-shield' ,text: 'ความปลอดภัย' ,link: '../../manage/security/set_password'},
            { icon:'fas fa-sliders-h' ,text: 'ระบบ' },
          ]},
        { icon: 'help', text: 'ช่วยเหลือ' },
        { icon: 'fas fa-sign-out-alt', text: 'ออกจากระบบ' },
        
      ]
    }),
    props: {
      source: String
    },
   
   /*methods: {
      students(){
        this.$router.replace('/student')
      },
      teacher(){
        this.$router.replace('/teacher')
      }
    }*/
  }
</script>
