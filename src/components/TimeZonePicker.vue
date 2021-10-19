<template>
    <div class="">
        <div style="min-width:170px;">
            <v-select
                :options="timeZones"
                @input="$emit('inputTimeZone', $event)"
                :value="timeZone"
            ></v-select>
        </div>
        <button type="button" class="btn btn-danger" @click="$emit('removeTimeZone', 'remove')">x</button>
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