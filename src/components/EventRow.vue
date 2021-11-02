<template>
    <tr class="mb-4">
        <td class="col">
            <div class="d-flex align-items-center">
                <font-awesome-icon
                    class="me-3 remove-button"
                    @click="removeEvent"
                    icon="times"
                />

                <input type="text" @input="$emit('updateName', $event)" />
            </div>
        </td>
        <td class="col">
            <input type="date" v-model="eventDate" />
        </td>
        <td v-for="(timeZone, index) in timeZones" :key="index">
            <TimePicker
                class="col"
                :key="index"
                :timeZone="timeZone"
                :date="eventDate"
                :momentTime="moment"
                @updateTime="updateTime"
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
            eventDate: "",
            moment: "",
        };
    },
    methods: {
        updateTime(response) {
            this.moment = moment.tz(
                this.eventDate + " " + response.time,
                response.timeZone
            );
        },
        removeEvent() {
            // destroy the vue listeners, etc
            this.$destroy();

            // remove the element from the DOM
            this.$el.parentNode.removeChild(this.$el);
        },
    },
    computed: {},
    created() {
        this.moment = moment();
        this.eventDate = this.moment.format("YYYY-MM-DD");
    },
    watch: {
        eventDate() {
            let newDate = moment(this.eventDate);
            let momentObject = newDate.toObject();

            this.moment.set({
                years: momentObject.years,
                months: momentObject.months,
                date: momentObject.date,
            });
        },
    },
};
</script>

<style>
.remove-button {
    color: rgb(34, 34, 34);
    font-size: 1.5em;
}
.remove-button:hover {
    color: rgb(156, 156, 156);
    cursor: pointer;
}
</style>