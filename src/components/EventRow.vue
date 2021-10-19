<template>
    <tr class="mb-4">
        <td class="col">
            <div class="d-flex align-items-center">
                <button
                    type="button"
                    class="btn btn-danger btn-sm mx-2"
                    @click="removeEvent"
                >
                    Delete
                </button>
                <input
                    type="text"
                    @input="$emit('updateName', $event)"
                />
            </div>
        </td>
        <td class="col">
            <input type="date" v-model="date" />
        </td>
        <td v-for="(timeZone, index) in timeZones" :key="index">
            <TimePicker
                class="col"
                :key="index"
                :timeZone="timeZone"
                :date="date"
                :momentTime="moment"
                @updateTime="updateMoment"
            />
        </td>
    </tr>
</template>

<script>
//MomentJs
import moment from "moment-timezone";

import TimePicker from "./subcomponents/TimePicker.vue";

export default {
    props: {
        timeZones: Array,
    },
    components: {
        TimePicker,
    },
    data() {
        return {
            date: "",
            moment: {},
        };
    },
    methods: {
        updateMoment(response) {
            this.moment = response;
        },
        removeEvent() {
            // destroy the vue listeners, etc
            this.$destroy();

            // remove the element from the DOM
            this.$el.parentNode.removeChild(this.$el);
        },
    },
    computed: {
        datetime: function () {
            let datetime = this.date + " " + this.time;

            if (moment(datetime, "YYYY-MM-DD HH:mm", true).isValid()) {
                return datetime;
            }

            return null;
        },
    },
    created() {
        this.moment = moment();
        this.date = this.moment.format("YYYY-MM-DD");
    },
    watch: {},
};
</script>

<style>
</style>