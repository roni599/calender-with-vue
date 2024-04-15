<template>
    <section>
        <section>
            <h1 class="text-center text-light text-uppercase fw-bold mt-5">My Vue Calender</h1>
        </section>
        <div class="container main d-flex mt-5">
            <div class="data_part">
                <section class="currentDay">
                    <p class="text-center fw-bold text-uppercase text-light">{{ currentDay }}</p>
                </section>
                <section class="currentDate">
                    <p class="text-center fw-bold text-light">{{ currentDate }}</p>
                </section>
            </div>
            <div class="calender_Part">
                <h1 class="text-center fw-bold text-info text-uppercase">{{ getMonth }} {{ currentYear }}</h1>
                <section>
                    <div class="days d-flex">
                        <p class="text-center" v-for="(day, index) in days" :key="index">
                            {{ day }}
                        </p>
                    </div>
                </section>
                <section>
                    <div class="dates d-flex">
                        <p class="text-center" v-for="day in getMonthFirstDays" :key="day"></p>
                        <p :class="todayDate(dates)" class="text-center" v-for="dates in lastDayOfMonth" :key="dates">{{ dates }}</p>

                    </div>
                </section>
                <section class="d-flex justify-content-between">
                    <button @click="Prev" class="btn  btn-primary">Prev</button>
                    <button @click="Next" class="btn  btn-primary">Next</button>
                </section>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: 'Calender-app',
    data() {
        return {
            days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
            currentInMonth: new Date().getMonth(),
            currentYear: new Date().getFullYear(),
            currentDate: new Date().getDate(),
            currentDay: new Date().toLocaleDateString('en-US', { weekday: 'long' })
        }
    },
    computed: {
        getMonth() {
            return new Date(this.currentYear, this.currentInMonth, this.currentDate).toLocaleString('default', { month: 'long' });
        },
        lastDayOfMonth() {
            return new Date(this.currentYear, this.currentInMonth + 1, 0).getDate();
        },
        getMonthFirstDays() {
            return new Date(this.currentYear, this.currentInMonth, 1).getDay();
        },
    },
    methods: {
        Next() {
            if (this.currentInMonth == 11) {
                this.currentInMonth = 0;
                this.currentYear++;
            }
            else {
                this.currentInMonth++
            }
        },
        Prev() {
            if (this.currentInMonth == 0) {
                this.currentInMonth = 11;
                this.currentYear--;
            }
            else {
                this.currentInMonth--;
            }
        },
        todayDate(data){
            let calender=new Date(this.currentYear,this.currentInMonth,data).toDateString();
            let today=new Date().toDateString();
            return calender===today? "text-light bg-primary":"";
        }
    }
}
</script>

<style>
.days p,
.dates p {
    width: 14.28%;
}

.calender_Part {
    width: 50%;
    padding: 20px;
    background-color: white;
}

.data_part {
    width: 50%;
    background-color: rgb(112, 220, 235);
}

.currentDay {
    font-size: 30px;
    font-weight: bold;
    margin-top: 30px;
}

.currentDate {
    font-size: 210px;
    margin-top: -60px;
}

.dates {
    flex-wrap: wrap;
}

.main {
    width: 100%;
}
</style>