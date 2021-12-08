<template>
    <div class="z-calendar">
        <!-- <v-container> -->
        <!--  optional: no-gutters,  class="fill-height" -->
        <v-row>
            <v-col
                cols="12"
                sm="6"
                md="2"
                lg="3"
                v-for="month in months"
                v-bind:key="month"
                class="month"
            >
                <v-sheet height="24">
                    <div class="month__title">{{ getMonthName(month) }}</div>
                </v-sheet>
                <v-sheet>
                    <!-- :min-weeks="6" -->
                    <v-calendar
                        ref="calendar"
                        :value="getCalendarMonth(month)"
                        :events="events"
                        color="primary"
                        type="month"
                        :weekdays="[1, 2, 3, 4, 5, 6, 0]"
                        :locale="getLocale()"
                        :show-month-on-first="false"
                        event-color="orange"
                    ></v-calendar>
                </v-sheet>
            </v-col>
        </v-row>
        <!-- </v-container> -->
    </div>
</template>

<script>
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
        // const months = ref(['2021-11-01', '2021-12-01', '2022-01-01']);
        const months = ref([-11, -10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2]);

        events.value = [
            {
                name: '',
                start: '2021-01-06',
                end: '2021-01-16',
            },
            {
                name: '',
                start: '2021-04-17',
                end: '2021-04-19',
            },
            {
                name: '',
                start: '2021-12-07',
                end: '2021-12-08',
            },
            {
                name: ``,
                start: '2021-11-06',
            },
            // {
            //     name: ``,
            //     start: '2021-11-06',
            // },
            {
                name: '',
                start: '2022-02-08',
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
        },
        getCalendarMonth(monthAdjust) {
            const now = new Date()
            return now.setMonth(now.getMonth() + monthAdjust)
        },
        getMonthName(month) {
            const cDate = this.getCalendarMonth(month)
            const objDate = new Date(cDate)
            return objDate.toLocaleString(this.getLocale(), { month: "long" });
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
        // margin-top: 24px;
    }
    .container {
        padding: 0;
        max-width: 100%;
    }
    .month__title {
        // margin-top: 12px;
        overflow: hidden;
    }
    .v-calendar.v-calendar-events .v-calendar-weekly__day {
        height: 3.5em;
        // overflow: hidden;
    }
    .v-btn--fab.v-size--small {
        height: 20px;
        width: 20px;
    }
    .v-event {
        margin: 0px 3px 3px 3px;
    }
    .v-event-more {
        background-color: red;
    }
}
</style>
