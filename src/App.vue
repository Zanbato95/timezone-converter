<template>
    <div id="app">
        <Header />
        <div class="container-fluid mt-3">
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">Name</th>
                        <th scope="col">Date</th>
                        <th
                            class="tabs"
                            v-for="(timeZone, index) in timeZones"
                            :key="index"
                        >
                            <TimeZonePicker
                                :timeZone="timeZone"
                                @inputTimeZone="updateTimeZone($event, index)"
                                @removeTimeZone="updateTimeZone($event, index)"
                            />
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <template v-for="(eventRow, index) in eventRows">
                        <EventRow :key="index" :timeZones="timeZones" />
                    </template>
                </tbody>
            </table>
        </div>
        <div class="app-buttons">
            <button
                type="button"
                class="btn btn-primary mx-2"
                @click="addNewEvent"
            >
                Add Event/Date
            </button>
            <button
                type="button"
                class="btn btn-success mx-2"
                @click="addTimeZone"
            >
                Add Timezone
            </button>
        </div>
    </div>
</template>

<script>
import moment from "moment-timezone";
import EventRow from "./components/EventRow.vue";
import TimeZonePicker from "./components/TimeZonePicker.vue";
import Header from "./components/Header.vue";

export default {
    name: "App",
    components: {
        EventRow,
        TimeZonePicker,
        Header,
    },
    data() {
        return {
            timeZones: [],
            eventRows: 0,
        };
    },
    methods: {
        addNewEvent() {
            this.eventRows++;
        },
        addTimeZone() {
            this.timeZones.push(null);
        },
        updateTimeZone(data, index) {
            if (data === "remove") {
                this.timeZones.splice(index, 1);
                return;
            }
            this.timeZones.splice(index, 1, data);
        },
    },
    created() {
        // Initialize timezone based on user location
        this.timeZones.push(moment.tz.guess());
        this.addNewEvent();
    },
};
</script>

<style scoped>
#app {
    margin-top: 5em;
}
.app-buttons {
    position: fixed;
    right: 3rem;
    bottom: 3rem;
}
</style>>

