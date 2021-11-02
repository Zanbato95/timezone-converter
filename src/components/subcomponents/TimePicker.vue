<template>
    <div>
        <input
            type="time"
            v-model="myTime"
            @input="update"
            :disabled="date === '' || timeZone === null"
        />
        <small v-show="myDate" class="text-muted px-2">({{ myDate }})</small>
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
            myTime: null,
            myDate: null,
            differentDate: false,
        };
    },
    methods: {
        update(event) {
            let response = {
                time: event.target.value,
                timeZone: this.timeZone,
            };

            this.$emit("updateTime", response);
        },
        updateTimepicker() {
            let cloneMoment = moment(this.momentTime);

            if (this.date === "" || this.timeZone === null) {
                this.myTime = null;
            } else {
                this.myTime = cloneMoment.tz(this.timeZone).format("HH:mm");
            }
        },
        updateMyDate() {
            let cloneMoment = moment(this.momentTime);

            if (
                this.timeZone == null ||
                cloneMoment
                    .tz(this.timeZone)
                    .isSame(moment.tz(this.date, this.timeZone), "day")
            ) {
                this.myDate = null;
            } else {
                this.myDate = cloneMoment
                    .tz(this.timeZone)
                    .format("MMM. DD, YYYY");
            }
        },
    },
    created() {
        this.updateTimepicker();
    },
    watch: {
        date() {
            this.updateTimepicker();
            this.updateMyDate();
        },
        momentTime() {
            this.updateTimepicker();
            this.updateMyDate();
        },
        timeZone() {
            this.updateTimepicker();
            this.updateMyDate();
        },
    },
};
</script>

<style>
</style>