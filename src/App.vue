<template>
  <div id="app">
    <styleEditor :code='currentStyle' ref='styleEditor'></styleEditor>
  </div>
</template>

<script>
    import styleEditor from './components/styleEditor'
    import './assets/reset.css'
    export default {
        name: 'app',
        components: {
            styleEditor
        },
        created: function() {
            this.progressivelyShowStyle();
        },
        data() {
            return {
                /*所有的style文件*/
                currentStyle: '',
                allStyles: `
                    /*
                    * Inspired by 
                    * https://github.com/Wscats/CV
                    * http://strml.net
                    * https://github.com/jirengu-inc/animating-resume
                    首先给所有元素加上过渡效果 */
                    * {
                      -webkit-transition: all .3s;
                      transition: all .3s;
                    }
                    /*设置字体颜色和html背景色*/
                    html {
                       color:rgb(222,222,222); 
                       background: rgb(0,43,54); 
                    }
                    /*把字体调大一点*/
                    #app{
                        font-size:18px;
                    }
                    /* 指定代码高亮颜色 */
                    .token.selector{ color: rgb(133,153,0); }
                    .token.property{ color: rgb(187,137,0); }
                    .token.punctuation{ color: yellow; }
                    .token.function{ color: rgb(42,161,152); }
                    /*调整文字和边框的距离*/
                    .styleEditor {
                        padding: .5em;
                        border: 1px solid white;
                        margin: .5em;
                        overflow: auto;
                        width: 45vw; 
                        height: 90vh;
                    }
                    /*加上3D效果，需要在Chrome浏览器下查看*/
                    html{
                      perspective: 1000px;
                      -webkit-perspective: 1000px;
                    }
                    .styleEditor {
                      position: fixed; left: 0; top: 0; 
                      transform: translateZ(-100px) rotateY(10deg);
                      -webkit-transform: translateZ(-100px) rotateY(10deg);
                    }
                    /*The End*/
                `
            }
        },
        methods: {
            progressivelyShowStyle: function() {
                /*按照一定时间间隔添加字符到currentStyle里面*/
                return new Promise((resolve, reject) => {
                    var showStyle = (async function() {
                        var allLength = this.allStyles.length;

                        if (this.currentStyle.length < allLength) {
                            var lastChar = this.allStyles[this.currentStyle.length - 1];
                            var char = this.allStyles[this.currentStyle.length] || ' ';
                            this.currentStyle += char;
                            if(lastChar==='\n'){
                               this.$nextTick(()=>this.$refs.styleEditor.wrap());
                               }
                            setTimeout(showStyle, 50);
                        } else {
                            resolve();
                        }
                    }).bind(this);

                    showStyle();
                });
            }
        }

    }

</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }

    html {
        min-height: 100vh;
    }

    * {
        -webkit-transition: all .3s;
        transition: all .3s;
    }

</style>
