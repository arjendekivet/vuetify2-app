<template>
    <div class="z-calendar">
        <!-- <v-container> -->
        <!--  optional: no-gutters -->
        <v-row>
            <v-col cols="12" md="6" lg="4" v-for="month in months" v-bind:key="month" class="month">
                <div class="month__title">{{ month }}</div>
                <v-calendar
                    ref="calendar"
                    :value="month"
                    :events="events"
                    color="primary"
                    type="month"
                    :weekdays="[1, 2, 3, 4, 5, 6, 0]"
                    :locale="getLocale()"
                    :show-month-on-first="false"
                ></v-calendar>
            </v-col>
        </v-row>
        <!-- </v-container> -->
        <!-- <div v-for="month in months" v-bind:key="month" class="month">
            <div></div>
            <v-calendar
                ref="calendar"
                :value="month"
                :events="events"
                color="primary"
                type="month"
                :weekdays="[1, 2, 3, 4, 5, 6, 0]"
                :locale="getLocale()"
                :show-month-on-first="true"
            ></v-calendar>
        </div>-->
    </div>
</template>

<script lang="ts">
import { ref } from '@vue/composition-api';

// type event = {
//     name: String,
//     start: String,
//     end?: String,
// }

export default {
    setup() {
        // const today = ref<Date>(new Date());
        // const events = ref<event[]>();
        const today = ref(new Date());
        const events = ref();
        const months = ref(['2021-11-01', '2021-12-01', '2022-01-01']);

        events.value = [
            {
                name: 'Weekly Meeting',
                start: '2021-12-07',
                end: '2021-12-08',
            },
            {
                name: `Thomas' Birthday`,
                start: '2019-01-10',
            },
            {
                name: 'Mash Potatoes',
                start: '2019-01-09 12:30',
                end: '2019-01-09 15:30',
            },
        ]

        return {
            today,
            events,
            months,
        };
    },
    //   components: { HelloWorld },
    methods: {
        getLocale() {
            return navigator.language
        }
    }
}
</script>

<style lang="scss">
.z-calendar {
    .month {
        // width: 300px;
        // margin: 12px;
        // border: 12px;
        margin-top: 24px;
    }
    .container {
        padding: 0;
        max-width: 100%;
    }
    .month__title {
        // margin-top: 12px;
        overflow: hidden;
    }
}
</style>
