<template>
    <card title="Custom input element">

        <input type="text" class="form-control form-control-lg" v-model="date" id="my-custom-input" placeholder="select date" style="max-width:250px">

        <date-picker
                v-model="date"
                format="jYYYY/jMM/jDD"
                element="my-custom-input"
        ></date-picker>
        <code class="code">{{ date }}</code>

        <template slot="code">
            <highlight-code lang="html" v-pre>
                &lt;input
                    type="text"
                    class="form-control form-control-lg"
                    v-model="date"
                    id="my-custom-input"
                    placeholder="select date"&gt;

                &lt;date-picker
                    v-model="date"
                    format="jYYYY/jMM/jDD"
                    element="my-custom-input"&gt;
                &lt;/date-picker&gt;
            </highlight-code>
        </template>
        <template slot="docs">
            <p>Sometime you need a custom input element:</p>
            <highlight-code lang="html">
                &lt;input type="text" name="my_date" class="my-custom-input"/&gt;
            </highlight-code>
            <p>define an <code class="inline">id</code> for it:</p>
            <highlight-code lang="html">
                &lt;input type="text" name="my_date" class="my-custom-input" id="my-custom-input-id"/&gt;
            </highlight-code>

            <p>then pass <code class="inline">id</code> to datepicker:</p>
            <highlight-code lang="html">
                &lt;date-picker v-model="..." format="..." element="my-custom-input-id"&gt;&lt;/date-picker&gt;
            </highlight-code>
        </template>
    </card>
</template>

<script>
    export default {
        data() {
            return {
                date: '',
            }
        },
    }
</script>