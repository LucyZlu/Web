<template>
    <div class='styleEditor' ref='container'>
        <div class="codeText" v-html="styleTagCode"></div>
        <pre v-html="highLightCode"></pre>
    </div>
</template>

<script>
    import Prism from 'prismjs'
    export default {
        name: 'styleEditor',
        props: ['code'],
        computed: {
            highLightCode: function() {
                return Prism.highlight(this.code, Prism.languages.css);
            },
            styleTagCode: function() {
                return `<style>${this.code}</style>`;
            }
        },
        methods:{
            /*拉动下滑框*/
            wrap:function(){
                this.$refs.container.scrollTop=100000;
            }
        }
    }

</script>

<style>
    .codeText {
        display: none;
    }

</style>
