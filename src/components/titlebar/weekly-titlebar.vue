<template>
    <!--头部最外层容器，定义盒子外观-->
    <!--main-title-wrap定义盒子外观，包括背景，高度，文本颜色和盒子阴影特效-->
    <!--wrap定义宽度100%，始终保持宽度覆盖整个屏幕-->
    <div class="main-title-wrap wrap">
        <!--头部实际内容区域-->
        <!--main-title-inner定义容器内各项在横轴和纵轴的对齐方式-->
        <!--inner定义内容区宽度为具体值960px，并且居中于外层容器-->
        <!--flex-container只干了一件事，将该块区域变为弹性盒子-->
        <!--flex-direction-row指明弹性盒子的方向为水平-->
        <div class="main-title-inner inner flex-container flex-direction-row">
            <!--实际内容区分为了两部分，除去登录|注册的部分和录|注册部分-->
            <!--除去登录|注册的部分-->
            <!--同样将该部分变为弹性盒子，并定义对齐方式-->
            <div class="main-title-left flex-container flex-direction-row">

                <!--logo部分，定义logo文本颜色和大小-->
                <div class="logo" @click="toHome"></div>
                <!--导航栏部分，变为弹性盒子，定义对齐方式，定义宽度和左边距-->
                <div class="title"> {{weeklyTitle}} </div>
            </div>
            <div class="actions" v-if="needActions">
                <div class="button-wrap flex-container flex-direction-row">
                    <div class="pre-look" @click="preLook">预览</div>
                    <div class="line"></div>
                    <div class="publish" @click="publish">发布</div>
                    <div class="line"></div>
                    <div class="download" @click="download">下载MD</div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import { mapState } from 'vuex';
    export default {
        props: {
            needActions: {
                type: Boolean,
                default: false
            }
        },
        computed: {
            ...mapState({
                weeklyTitle: state => state.weeklyState.weeklyTitle
            })
        },
        methods: {
            toHome () {
                location.href = './index.html';
            },
            preLook () {
                this.$emit('preLook');
            },
            publish () {
                this.$emit('publish');
            },
            download () {
                this.$emit('download');
            }
        }
    };
</script>
<style scoped>
    .main-title-wrap {
        background-color: #fff;
        height: 60px;
        color: #71777c;
        -webkit-box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        -moz-box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    }

    .main-title-inner {
        /* align-items 属性定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式,使用每个弹性对象元素的 align-self 属性可重写 align-items 属性 */

        /* IE 10 及更早版本浏览器不支持 align-items 属性, Safari 7.0 及更新版本通过 -webkit-align-items 属性支持该属性 */
        align-items: center;

        /* justify-content 用于设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式 */

        /* space-between表示项目位于各行之间留有空白的容器内,即首尾两个顶住两头，中间各项均匀分布 */
        justify-content: space-between;
    }

    .main-title-left {
        align-items: center;
    }

    .logo {
        /* color: #007fff; */

        /* 感觉这里line-height可以不需要，不影响效果。而且这个值如果超过了头部高度，还会对样式产生影响 */

        /* line-height: 60px; */

        /* font-size: 30px; */
        width: 193px;
        height: 60px;
        background: transparent url(~assets/img/face.png) no-repeat;
        background-size: cover;
        cursor: pointer;
    }

    .title {
        margin-left: 30px;
        font-size: 25px;
        color: #000;
    }

    .button-wrap {
        width: 180px;
        justify-content: space-between;
        text-decoration: underline;
    }

    .button-wrap > div {
        cursor: pointer;
    }

    .line {
        width: 1px;
        height: 20px;
        background-color: #ccc;
    }

</style>