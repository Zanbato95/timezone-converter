<template>
    <div class="d-inline-flex justify-content-center align-items-center">
        <span style="min-width: 240px; margin-right: 10px">
            <v-select
                :options="timeZones"
                @input="$emit('inputTimeZone', $event)"
                :value="timeZone"
            ></v-select>
        </span>
        <a type="button" @click="$emit('removeTimeZone', 'remove')">x</a>
    </div>
</template>

<script>
//Vue-select
import vSelect from "vue-select";
import "vue-select/dist/vue-select.css";

//MomentJs
import moment from "moment-timezone";

export default {
    props: {
        timeZone: String,
    },
    components: {
        vSelect,
    },
    data() {
        return {
            timeZones: [], // init timeZones array
        };
    },
    created() {
        this.timeZones = moment.tz.names(); // get list of timeZones from moment
    },
};
</script>