<template>
    <v-card elevation="3" style="height: 96vh">
        <v-tabs v-model="tab" bg-color="deep-purple-accent-4" centered>
            <v-tab value="tab-1">
                General
            </v-tab>
            <v-tab value="tab-2">
                Request
            </v-tab>
            <v-tab value="tab-3">
                Response
            </v-tab>
        </v-tabs>

        <v-window v-model="tab">
            <v-window-item value="tab-1">
                <v-card class="pa-3">
                    <JsonVisualizer :data="generalData" target="target1" />
                </v-card>
            </v-window-item>
            <v-window-item value="tab-2">
                <v-card class="pa-3">
                    <JsonVisualizer :data="requestData" target="target2" />
                </v-card>
            </v-window-item>
            <v-window-item value="tab-3">
                <v-card class="pa-3">
                    <JsonVisualizer :data="responseData" target="target3" />
                </v-card>
            </v-window-item>
        </v-window>
    </v-card>
</template>

<script>
import JsonVisualizer from './JsonVisualizer.vue'

export default {
    data() {
        return {
            tab: null,
            generalData: [],
            responseData: [],
            requestData: []
        };
    },
    props: ["jsonData"],
    updated() {
        let general = {
            url: this.jsonData.url,
            method: this.jsonData.method,
            status: this.jsonData.status,
            name: this.jsonData.name,
        };
        let response = {
            header: this.jsonData.res_header,
            body: this.jsonData.res_body
        };
        let request = {
            header: this.jsonData.req_header,
            body: this.jsonData.req_body
        };
        this.generalData = general;
        this.responseData = response;
        this.requestData = request;
    },
    components: { JsonVisualizer }
}
</script>

<style>

</style>