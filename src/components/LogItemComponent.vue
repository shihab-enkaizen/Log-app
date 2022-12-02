<template>
    <v-card elevation="1" class="pa-1 ">
        <v-row style="cursor:pointer">
            <v-col cols="2" class="d-flex justify-center align-center">
                <span class="px-1 rounded-lg" :class="'bg-' + colors[status]">{{ status }}</span>
            </v-col>
            <v-col cols="10" class="pl-0">
                <v-tooltip :text="url">
                    <template v-slot:activator="{ props }">
                        <div class="d-flex flex-column" v-bind="props">
                            <span>{{ title }}</span>
                            <span>{{ url.substring(0, 42) }}</span>
                        </div>
                    </template>
                </v-tooltip>
            </v-col>
        </v-row>
    </v-card>
</template>

<script>
export default {
    props: ["title", "url", "status"],
    data() {
        return {
            colors: {
                200: "green",
                404: "deep-orange",
                500: "deep-orange"
            }

        }
    },
    // mounted() {
    //     this.url = this.url.substring(0, 10)
    // },
}
</script>

<style>

</style>