<template>
    <v-tab :items="items">
        <div slot="toMarkdown">
            <v-input-txt label="HTML" v-model="htmlText1" placeholder="HTML"></v-input-txt>
            <div class="layui-form-item layui-form-text">
                <div class="layui-input-block">
                    <v-button icon="down" @click="toMarkdown()">转为Markdown</v-button>
                </div>
            </div>
            <v-input-txt label="MarkDown"  v-bind:value="mdText1" placeholder="MarkDown"></v-input-txt>
        </div>
        <div slot="toHtml">
            <v-input-txt label="Markdown" v-model="mdText2" placeholder="MarkDown"></v-input-txt>
            <div class="layui-form-item layui-form-text">
                <div class="layui-input-block">
                    <v-button icon="down" @click="toHtml()">转为Html</v-button>
                </div>
            </div>
            <v-input-txt label="Html"  v-bind:value="htmlText2" placeholder="Html"></v-input-txt>
            <h2 class="site-tips">预览</h2>
            <div v-html="htmlText2" class="layui-input-block artcontent" >
            </div>
        </div>
    </v-tab>
</template>
<script>
    import '../assets/css/markdown.css'
    import toMarkdown from '../utils/tomarkdown'
    export default {
        data () {
            return {
                items:[
                    {
                        Title:'Html转Markdown',
                        Name:'toMarkdown'
                    },
                    {
                        Title:'Markdown转Html',
                        Name:'toHtml'
                    },
                    {
                        Title:'查看代码',
                        Name:'code',
                        Url:'http://coding.net/u/yimocoding/p/metools/git/blob/master/src/pages/mdconvert.vue',
                    }
                ],
                htmlText1:'',
                mdText1:'',
                mdText2:'',
                htmlText2:''
            }
        },
        methods: {
            convert(md){
                var marked = require('marked');
                marked.setOptions({
                    renderer: new marked.Renderer(),
                    gfm: true,
                    tables: true,
                    breaks: false,
                    pedantic: false,
                    sanitize: false,
                    smartLists: true,
                    smartypants: false
                });
                return marked(md);
            },
            toHtml(){
                this.htmlText2=this.convert(this.mdText2);
            },
            toMarkdown(){
                this.mdText1=toMarkdown.toMarkdown(this.htmlText1)
            }
        }

    }
</script>