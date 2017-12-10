<template>
    <div class='styleEditor'>
    <div class="codeText" v-text="styleTagCode"></div>
    <div class="" v-html="styleTagCode"></div>
    </div>
</template>

<script>
    export default {
        name: 'styleEditor',
        props: ['code'],
        computed: {
            styleTagCode: function() {
                return '<style>' + this.code + '</style>';
            }
        }
    }

</script>
