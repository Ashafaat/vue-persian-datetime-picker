<template>
    <card title="Highlight" version="1.1.5">


        <div class="mt-5">
            <date-picker
                    v-if="tab=='d'"
                    key="d"
                    initialValue="1397/12/12"
                    :highlight="highlightDay"
            ></date-picker>

            <date-picker
                    v-if="tab=='y'"
                    key="y"
                    initialValue="1397"
                    type="year"
                    :highlight="highlightYear"
            ></date-picker>

            <date-picker
                    v-if="tab=='m'"
                    key="m"
                    initialValue="05"
                    type="month"
                    :highlight="highlightMonth"
            ></date-picker>

            <date-picker
                    v-if="tab=='t'"
                    key="t"
                    initialValue="22:22"
                    type="time"
                    :highlight="highlightTime"
            ></date-picker>

            <date-picker
                    v-if="tab=='dt'"
                    key="dt"
                    initialValue="1397/05/06 22:00"
                    type="datetime"
                    :highlight="highlightDatetime"
            ></date-picker>
        </div>


        <template slot="code">

            <div class="btn-group mb-2">
                <span v-for="btn,k in buttons" class="btn" :class="tab===k ?'btn-info':'btn-secondary'" @click="tab=k">{{ btn }}</span>
            </div>

            <template v-if="tab=='d'">
                <highlight-code lang="html" v-pre>
                    &lt;date-picker :highlight="highlight"&gt;&lt;/date-picker&gt;
                </highlight-code>
                <highlight-code lang="javascript" v-pre>
                    methods: {
                        highlight(formatted, dateMoment, checkingFor) {
                            let attributes = {'title': 'Today is ' + formatted};
                            if (checkingFor === 'day' && formatted === '1397/12/28'){
                                attributes['class'] = 'highlighted-1';
                                attributes['title'] = 'جشن چهارشنبه سوری';
                            }
                            if (checkingFor === 'day' && formatted === '1397/12/29'){
                                attributes['class'] = 'highlighted-2';
                                attributes['title'] = 'روز ملی شدن صنعت نفت';
                            }
                            return attributes;
                        }
                    }
                </highlight-code>
                <highlight-code lang="scss">
                    .highlighted-1 {
                        > span {  color: #EF6C00 !important;  }
                        .{{ $prefix }}day-effect {
                            background-color: #f9e1be !important;
                            border: solid 1px #EF6C00;
                        }
                    }
                    .highlighted-2 {
                        color: #E91E63;
                        .{{ $prefix }}day-effect {  background-color: #E91E63 !important;  }
                    }
                </highlight-code>
            </template>

            <template v-if="tab=='y'">
                <highlight-code lang="html" v-pre>
                    &lt;date-picker type="year" :highlight="highlight"&gt;&lt;/date-picker&gt;
                </highlight-code>
                <highlight-code lang="javascript" v-pre>
                    methods: {
                        highlight(formatted, dateMoment, checkingFor) {
                            if (checkingFor === 'year' && formatted === '1396') return {
                                'style': {'color': 'red !important'},
                                'class': 'highlighted',
                                'data-info': '1396',
                            };
                            return {}
                        }
                    }
                </highlight-code>
            </template>

            <template v-if="tab=='m'">
                <highlight-code lang="html" v-pre>
                    &lt;date-picker type="month" :highlight="highlight"&gt;&lt;/date-picker&gt;
                </highlight-code>
                <highlight-code lang="javascript" v-pre>
                    methods: {
                        highlight(formatted, dateMoment, checkingFor) {
                            if (formatted === '05') return {
                                'style': {'color': 'red !important'},
                                'class': 'highlighted',
                            };
                            return {}
                        }
                    }
                </highlight-code>
            </template>

            <template v-if="tab=='t'">
                <highlight-code lang="html" v-pre>
                    &lt;date-picker type="time" :highlight="highlight"&gt;&lt;/date-picker&gt;
                </highlight-code>
                <highlight-code lang="javascript" v-pre>
                    methods: {
                        highlight(formatted, dateMoment, checkingFor) {
                            if (dateMoment.hour() === dateMoment.minutes()) return {
                                'style': {'color': '#00BCD4 !important'}
                            };
                            return {}
                        }
                    }
                </highlight-code>
            </template>

            <template v-if="tab=='dt'">
                <highlight-code lang="html" v-pre>
                    &lt;date-picker type="datetime" :highlight="highlight"&gt;&lt;/date-picker&gt;
                </highlight-code>
                <highlight-code lang="javascript" v-pre>
                    methods: {
                        highlightDatetime(formatted, dateMoment, checkingFor) {
                            if (checkingFor === 'time' && dateMoment.format('HH:mm') === '22:00')
                                return {'style': {'color': '#ff9800 !important'}};
                            else if (checkingFor === 'day' && dateMoment.jDate() === 5)
                                return {'class': 'highlighted-1'};
                            return {}
                        }
                    }
                </highlight-code>
            </template>


        </template>
    </card>
</template>

<script>
    import moment from 'moment-jalaali';
    export default {
        data() {
            return {
                tab: 'd',
                buttons: {
                    y: 'Year',
                    m: 'Month',
                    d: 'Date',
                    t: 'Time',
                    dt: 'DateTime',
                }
            }
        },
        methods: {
            highlightDay(formatted, dateMoment, checkingFor) {
                let attributes = {'title': 'Today is ' + formatted};
                if (checkingFor === 'day' && formatted === '1397/12/28'){
                    attributes['class'] = 'highlighted-1';
                    attributes['title'] = 'جشن چهارشنبه سوری';
                }
                if (checkingFor === 'day' && formatted === '1397/12/29'){
                    attributes['class'] = 'highlighted-2';
                    attributes['title'] = 'روز ملی شدن صنعت نفت';
                }
                return attributes;
            },
            highlightYear(formatted, dateMoment, checkingFor) {
                if (checkingFor === 'year' && formatted === '1396') return {
                    'style': {'color': 'red !important'},
                    'class': 'highlighted',
                    'data-info': '1396',
                };
                return {}
            },
            highlightMonth(formatted, dateMoment, checkingFor) {
                if (formatted === '05') return {
                    'style': {'color': 'red !important'},
                    'class': 'highlighted',
                };
                return {}
            },
            highlightTime(formatted, dateMoment, checkingFor) {
                if (dateMoment.hour() === dateMoment.minutes()) return {
                    'style': {'color': '#00BCD4 !important'}
                };
                return {}
            },
            highlightDatetime(formatted, dateMoment, checkingFor) {
                if (checkingFor === 'time' && dateMoment.format('HH:mm') === '22:00')
                    return {'style': {'color': '#ff9800 !important'}};
                else if (checkingFor === 'day' && dateMoment.jDate() === 5)
                    return {'class': 'highlighted-1'};
                return {}
            },
        }
    }
</script>
<style lang="scss">
    .highlighted-1 {
        > span {  color: #EF6C00 !important;  }
        .vpd-day-effect {
            background-color: #f9e1be !important;
            border: solid 1px #EF6C00;
        }
    }
    .highlighted-2 {
        color: #E91E63;
        .vpd-day-effect {  background-color: #E91E63 !important;  }
    }
</style>