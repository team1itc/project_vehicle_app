<template>
    <div>
      <v-layout justify-center>
    <v-flex xs12 sm8>
      <v-card>
        <v-card-title >
            
          <span class="tada animated">
            <v-text class="title">
            หน้าแรก
            </v-text>
          </span>
        </v-card-title>
        <v-container
          fluid
          grid-list-md
        >
          <v-layout row wrap>
            <v-flex
              v-for="card in cards"
              v-bind="{ [`xs${card.flex}`]: true }"
              :key="card.title"
            >
              <v-card>
                <v-card-media
                  :src="card.src"
                  height="200px" class="slideInLeft animated"
                >
                  <v-container
                    fill-height
                    fluid
                    pa-2>
                  </v-container>
                </v-card-media>

                <v-card-actions>
                  <v-spacer></v-spacer>
                </v-card-actions>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>

        <v-list>
          <v-list-tile >
            <v-list-tile-action>
              <v-icon class="zoomInDown animated">person</v-icon>
            </v-list-tile-action>

            <v-list-tile-content>
              <v-list-tile-title class="zoomInDown animated">siriluk jansee</v-list-tile-title>
            </v-list-tile-content>
           
          </v-list-tile>

                    <v-divider inset></v-divider>

          <v-list-tile >
            <v-list-tile-action>
              <v-icon color="amber" class="zoomInDown animated">fas fa-motorcycle fa-2x</v-icon>
            </v-list-tile-action>

            <v-list-tile-content>
              <v-list-tile-title class="zoomInDown animated">DD-123</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>

        </v-list>

          <v-divider inset></v-divider>

          <v-list-tile >
            <v-list-tile-action>
              <v-icon color="red darken-4" class="zoomInDown animated">location_on</v-icon>
            </v-list-tile-action>

            <v-list-tile-content>
              <v-list-tile-title class="zoomInDown animated">จ.ชัยภูมิ </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>


        <v-card-media></v-card-media>
      
      </v-card>
    </v-flex>
  </v-layout>
    </div>
</template>
<script>
export default {
  layout: 'main_layout',
  data() {
    return {
      id: 1,
    }
  },
  data: () => ({
      cards: [
        { src: 'image/cc.jpg', flex: 12 }
      ]
    })
}
</script>