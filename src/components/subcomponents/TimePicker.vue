<template>
    <div>
        <input
            type="time"
            v-model="mytime"
            @input="update"
            :disabled="date === '' || timeZone === null"
        />
    </div>
</template>

<script>
//MomentJs
import moment from "moment-timezone";

export default {
    props: {
        timeZone: String,
        date: String,
        momentTime: Object,
    },
    data() {
        return {
            mytime: null,
        };
    },
    methods: {
        update(event) {
            let momentTime = moment.tz(
                this.date + " " + event.target.value,
                this.timeZone
            );

            this.$emit("updateTime", momentTime);
        },
    },
    created() {
        this.mytime = this.momentTime.tz(this.timeZone).format("HH:mm");
    },
    watch: {
        momentTime() {
            this.mytime = this.momentTime.tz(this.timeZone).format("HH:mm");
        },
        timeZone() {
            this.mytime = this.momentTime.tz(this.timeZone).format("HH:mm");
        },
    },
};
</script>

<style>
</style>