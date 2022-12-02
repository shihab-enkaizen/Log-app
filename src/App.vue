<template>
  <!-- <p class="text-h4 text-center pa-5 font-weight-bold text-indigo-lighten-5">Logz</p> -->
  <v-container fluid>
    <v-row>
      <v-col cols="4">
        <v-tabs v-model="tab" bg-color="deep-purple-accent-4" centered>
          <v-tab value="tab-1">
            Incoming
          </v-tab>
          <v-tab value="tab-2">
            Outgoing
          </v-tab>
        </v-tabs>
        <v-window v-model="tab">
          <v-window-item value="tab-1">
            <!-- child component 1 -->
            <LogListComponent @getJson="getJson" />
          </v-window-item>
          <v-window-item value="tab-2">
            <v-card>
              <v-card-text>
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Laborum at libero voluptatibus
                repudiandae illo minima commodi fugiat eaque tempora, ut suscipit ad nihil in corporis numquam incidunt!
                Repellat, possimus! Similique!
              </v-card-text>
            </v-card>
          </v-window-item>
        </v-window>

      </v-col>
      <v-col cols="8" class="">
        <!-- child component 2 -->
        <JsonViewComponent :jsonData="data" @getJson="data = $event" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import JsonViewComponent from './components/JsonViewComponent.vue'
import LogListComponent from './components/LogListComponent.vue'
export default {
  components: { LogListComponent, JsonViewComponent },
  data() {
    return {
      tab: null,
      data: {}
    }
  },
  methods: {
    getJson(event) {
      this.data = event
    }
  }



}
</script>

<style>

</style>