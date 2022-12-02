<template>
    <v-card style="border-radius:0px;">
        <v-banner :sticky="sticky" lines="one">
            <v-row>
                <v-col cols="9" class="pl-1">
                    <v-card-text class="pa-0">
                        <v-text-field :loading="loading" density="compact" variant="solo" label="Search" single-line
                            hide-details @keyup="onClick">
                        </v-text-field>
                    </v-card-text>
                </v-col>
                <v-col cols="3" class="pl-0">
                    <v-select label="Select" :items="requestMethods" variant="solo" density="compact"></v-select>
                </v-col>
            </v-row>
        </v-banner>
    </v-card>
    <v-card style="height: 81vh; border-top-left-radius: 0px 0px;" class="pa-3 pt-0 overflow-auto">
        <div class="d-flex flex-column " style="gap:20px">
            <LogItemComponent v-for="(log, index) in logs" :key="index" :title="log.data.name" :url="log.data.url"
                :status="log.data.status" @click="assignLog(log, index)"
                :class="(selectedIndex != -1 && index == selectedIndex) ? 'active' : ''" />
        </div>
    </v-card>
</template>

<script>
import LogItemComponent from './LogItemComponent.vue';



export default {
    components: { LogItemComponent },
    data() {
        return {
            logs: [
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example-asda-adsadkalksdlkasd-alkdwlakdlak-dsalkdlawi-dwalikl.com",
                        method: "post",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Change User Information",
                        req_header: {
                            dummy: "testing req_headers 2"
                        },
                        req_body: {
                            dummy: "Testing req_body 2"
                        },
                        res_header: {
                            dummy: "testing res_headers 2 "
                        },
                        res_body: {
                            dummy: "Testing res_body 2"
                        },
                        status: 404,
                        url: "http://www.example.com",
                        method: "get",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Update address",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "put",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Calculate Cost",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "delete",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Show Area",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 500,
                        url: "http://www.example.com",
                        method: "post",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "List shops",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "get",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "put",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "delete",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "post",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 500,
                        url: "http://www.example.com",
                        method: "get",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "delete",
                    }
                },
                {
                    type: "incoming",
                    data: {
                        name: "Submit Form",
                        req_header: {
                            dummy: "testing req_headers"
                        },
                        req_body: {
                            dummy: "Testing req_body"
                        },
                        res_header: {
                            dummy: "testing res_headers"
                        },
                        res_body: {
                            dummy: "Testing res_body"
                        },
                        status: 200,
                        url: "http://www.example.com",
                        method: "get",
                    }
                },
            ],
            requestMethods: ['GET', 'POST', 'PUT', 'DELETE'],
            selectedIndex: -1,
            loaded: false,
            loading: false,
            sticky: true
        }
    },
    methods: {
        assignLog(log, index) {
            this.$emit("getJson", log.data)
            this.selectedIndex = index
        },
        onClick() {
            this.loading = true
            setTimeout(() => {
                this.loading = false
                this.loaded = true
            }, 1000)
        },
    },


}
</script>

<style scoped>
.active {
    background-color: rgb(254, 156, 156);
}
</style>