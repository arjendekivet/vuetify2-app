<template>
    <div class="z-calendar">
        <div class="z-calendar__body">
            <!-- <v-container> -->
            <!--  optional: no-gutters,  class="fill-height" -->
            <v-row :no-gutters="!gutters">
                <v-col
                    cols="12"
                    sm="6"
                    md="2"
                    lg="3"
                    v-for="month in months"
                    v-bind:key="month"
                    class="month"
                >
                    <v-sheet height="40" class="month__title__bar">
                        <div class="month__title">{{ getMonthTitle(month) }}</div>
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
        <div>LEGEND</div>
    </div>
</template>

<script lang="ts">
import { ref } from '@vue/composition-api';

interface event {
    name: String,
    start: String,
    end?: String,
}

const mockEvents: event[] = [
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
    {
        name: ``,
        start: '2021-11-06',
    },
    {
        name: '',
        start: '2022-02-08',
    },
]

export default {
    props: {
        gutters: Boolean
    },
    setup() {
        const today = ref<Date>(new Date());
        const events = ref<event[]>();
        const months = ref([-11, -10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0]);

        events.value = mockEvents

        return {
            today,
            events,
            months,
        };
    },
    methods: {
        getLocale(): string {
            return navigator.language
        },
        getCalendarMonth(monthAdjust: number): number {
            const now = new Date()
            return now.setMonth(now.getMonth() + monthAdjust)
        },
        getMonthTitle(monthAdjust: number): string {
            const cDate = this.getCalendarMonth(monthAdjust)
            const objDate = new Date(cDate)
            return objDate.toLocaleString(this.getLocale(), { month: "long", year: 'numeric' });
        }
    }
}
</script>

<style lang="scss">
.z-calendar {
    margin: 10px;

    .z-calendar__body {
        border: solid 1px lightgrey;
        padding: 2px;
    }
    .container {
        padding: 0;
        max-width: 100%;
    }
    .month__title__bar {
        &.v-sheet {
            background-color: darkgray;
            text-align: center;
            line-height: 40px;
            color: #ffffff;
            margin-bottom: 5px;
        }
    }
    .month__title {
        overflow: hidden;
        font-weight: 700;
    }
    .v-calendar.v-calendar-events .v-calendar-weekly__day {
        // height: 3.5em;
        // overflow: hidden;
    }
    .v-calendar .v-btn {
        font-weight: 400;
        z-index: 2;
        margin-bottom: 1px;
    }
    .v-btn--fab.v-size--small {
        height: 20px;
        width: 20px;
    }
    .v-event {
        margin: 0px 3px 3px 1px;
    }
    .v-calendar.v-calendar-events .v-event-more {
        display: none;
    }
    .v-calendar.v-calendar-weekly .v-calendar-weekly__day {
        border-right: 0;
        border-bottom: 0;
        color: darkgray;
    }
    .v-calendar.v-calendar-events .v-calendar-weekly__day {
        margin-right: 0px;
    }
    .v-calendar.v-calendar-weekly .v-calendar-weekly__day.v-outside {
        visibility: hidden;
    }
    .v-calendar.v-calendar-weekly .v-calendar-weekly__head-weekday.v-outside {
        background-color: transparent;
    }
    .v-calendar.v-calendar-weekly .v-calendar-weekly__head-weekday.v-past {
        color: darkgray;
    }
    .v-calendar.v-calendar-weekly .v-calendar-weekly__head-weekday {
        border-right: 0;
    }
    .v-calendar.v-calendar-events .v-calendar-weekly__head-weekday {
        margin-right: 0px;
    }
    .v-calendar.v-calendar-weekly {
        border-top: 0;
        border-left: 0;
        padding-left: 10px;
    }
    .v-calendar .v-event {
        margin-top: -22px;
        // z-index: 1;
    }
}
</style>
