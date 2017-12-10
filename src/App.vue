<template>
  <div id="app">
    <styleEditor :code='currentStyle'></styleEditor>
  </div>
</template>

<script>
    import styleEditor from './components/styleEditor'

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
                allStyles: `.{
                        padding: 0;
                        margin: 0;
                    }
                    html {
                       color:rgb(222,222,222); 
                       background: rgb(0,43,54); 
                       
                    }
                    .styleEditor {
                        padding: .5em;
                        border: 1px solid white;
                        margin: .5em;
                        overflow: auto;
                        width: 45vw; height: 90vh;
                    }
                    /*加上3D效果*/
                    html{
                      perspective: 1000px;
                      -webkit-perspective: 1000px;
                    }
                    .styleEditor {
                      position: fixed; left: 0; top: 0; 
                      transform: translateZ(-100px) rotateY(10deg);
                      -webkit-transform: translateZ(-100px) rotateY(10deg);
                    }
                    /*The end*/
                `
            }
        },
        methods: {
            progressivelyShowStyle: function() {
                /*按照一定时间间隔添加字符到currentStyle里面*/
                var self = this;
                return new Promise((resolve, reject) => {
                    var showStyle = function() {
                        var allLength = self.allStyles.length;
                        if (self.currentStyle.length < allLength) {
                            var char = self.allStyles[self.currentStyle.length];
                            self.currentStyle += char;
                            setTimeout(showStyle, 50);
                        } else {
                            resolve();
                        }
                    }
                    showStyle();
                });
            }
        }

    }

</script>
