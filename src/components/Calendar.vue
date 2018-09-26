<template>
    <div>
        <div class="calendar">
            <div class="calendar__head">
                <vs-button v-on:click="monthPrev" vs-type="filled" class="button">前月</vs-button>
                <p>{{year}}年{{month}}月</p>
                <vs-button v-on:click="monthNext" vs-type="filled" class="button">次月</vs-button>
            </div>
            <ul class="weeks">
                <li class="weeks__item" v-for="week in weekList">{{week}}</li>
            </ul>
            <ul class="days">
                <li class="day__item" v-for="(day,index) in dayList" v-bind:key="day.id" v-bind:style="[ index === 0 ?{gridColumn:gridStart + '/' + gridEnd}:'']">
                    {{day.day}}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Calendar",
        data: function () {
            return {
                active: true,
                today: 0,
                year: 0,
                month: 0,
                dayList: [],
                weekList: ['日', '月', '火', '水', '木', '金', '土'],
                lastDay: 0,
                firstDay: 0,
                weekday: 0,
                gridStart: 0,
                gridEnd: 1
            }
        },
        created: function () {
            this.today = new Date();
            this.year = this.today.getFullYear();
            this.month = this.today.getMonth() + 1;
        },
        // computed: {
        //     //今日の日付データを取得
        //     today: function () {
        //         return new Date();
        //     },
        //     //今日の日付から年を取得
        //     year: function () {
        //         return this.today.getFullYear();
        //     },
        //     //今日の日付から月を取得
        //     month: function () {
        //         return this.today.getMonth() + 1;
        //     }
        // },
        watch: {
            month: {
                handler: function () {
                    this.firstDay = new Date(this.year, (this.month - 1), 1);
                    this.lastDay = new Date(this.year, (this.firstDay.getMonth() + 1), 0).getDate();
                    this.weekday = this.firstDay.getDay();
                    this.gridStart = this.weekday + 1;
                    this.gridEnd = this.gridStart + 1;
                    this.dayList = [];
                    let weekday = this.weekday
                    for (let i = 0; i < this.lastDay; i++) {
                        this.dayList[i] = {
                            day: i + 1,
                            weekday: weekday
                        };
                        if(weekday < 6) {
                            weekday += 1
                        } else {
                            weekday = 0;
                        }
                    }
                },
                immediate: true
            },
            // month: function () {
            //     this.dayList = [];
            //     for (let i = 1; i <= this.lastDay; i++) {
            //         this.dayList.push(i)
            //     }
            // }
        },
        methods: {
            monthNext: function () {
                if (this.month < 12) {
                    this.month += 1;
                } else {
                    this.month = 1;
                    this.year += 1;
                }

            },
            monthPrev: function () {
                if (this.month > 1) {
                    this.month -= 1;
                } else {
                    this.month = 12;
                    this.year -= 1;
                }
            }
        }

    }
</script>

<style scoped>
    .calendar {
        display: grid;
        width: 500px;
        margin: auto;
    }

    .weeks, .days {
        display: grid;
        grid-template-columns: repeat(7, 1fr);
        justify-content: space-between;
        margin: 0;
    }

    .day__item {
        padding: 5px 0;
    }

    ul {
        list-style: none;
        padding: 0;
    }

    .calendar__head {
        display: flex;
        width: 100%;
        align-items: center;
        justify-content: space-between;
        margin: 0 0 20px;
    }

    .button {
        width: 70px;
    }
</style>