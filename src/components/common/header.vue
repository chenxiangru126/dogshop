<template>
    <div class="header_b">
        <div class="ios_log" v-show="isIos"></div>
        <div class="w rela">
            <div class="_left" v-if='route_name=="switch"||route_name=="shopping_list"||route_name=="order_list_buyer"||route_name=="detailData"||route_name=="register"||route_name=="goods-class"||route_name=="goods-details-sCart"' @click='back_ios'></div>
            <div class="_left" v-else @click='back_event'></div>
            <div class="w t-c _center">{{title_name}}</div>
            <div class=" _right flex-v flex-j-c flex-a-c" v-if='route_name=="order_list_seller"||route_name=="order_list_buyer"' @click="order_search">
                <img src="../../static/images/search.svg" alt="" class="w1_5 h1_5">
            </div>
    
            <div class=" _right flex-v flex-j-c flex-a-c" v-if='route_name=="wallet"' @click="go_mx">
                <img src="../../static/images/mx-icon.png" alt="" class="mx-btn">
            </div>
            <div class=" _right flex-v flex-j-c flex-a-c c6" v-if='route_name=="address_list"' @click="address_chick">
                <span v-if="address_checked">全不选</span>
                <span v-else>全选</span>
            </div>
            <div class=" _right flex-v flex-j-c flex-a-c c6" v-if='route_name=="library-into"'>
                <span >一键导入      </span>
            </div>
        </div>
    </div>
</template>



<script>
    import {
        isAndroidOrIos
    } from '../../libs/tools';
    import {
        mapState
    } from 'vuex';
    import ios from "../../libs/ios";
    export default {
        data() {
            return {
                title: this.$route.meta.title,
                isIos: isAndroidOrIos() == 1 ? true : false,
                //地址列表-删除功能-【全选／全不选】状态切换-参数
                address_checked: false, //false 全不选  true 全选
                isShow:true
            }
        },
        computed: mapState(
            ['title_name', 'route_name']
        ),
        // watch:{
        //     $route(now,old){     //监控路由变换，控制返回按钮的显示
        //         if(old.path!="/"){
        //             this.isShow=false;
        //         } else{
        //             this.isShow=true;
        //         }
        //     }
        // },
        created() {
            // 定义全局函数，负责接收平级组件传递的参数
            this.$root.eventHup.$on('childEvent', this.process_child_event);
    
        },
        mounted() {
            var that = this;
        },
        methods: {
            order_search() {
                if (this.route_name == 'order_list_seller') {
                    this.$router.push({
                        name: 'order_search_seller'
                    })
                } else if (this.route_name == 'order_list_buyer') {
                    this.$router.push({
                        name: 'order_search_buyer'
                    })
                }
            },
            back_event() {
                history.back();
            },
            back_ios() {
                try {
                    iosObject.closeHtml();
                } catch (error) {
                    alert(error);
                }
            },
            process_child_event(content) {
                // 处理地址列表，全选状态，接收参数
                if (this.route_name == 'address_list') {
                    this.address_checked = content.address_checked
                }
            },
            address_chick() {
                this.address_checked = !this.address_checked;
                this.$root.eventHup.$emit('receive_address_check', this.address_checked)
            },
            go_mx() {
                this.$router.push({
                    name: 'tx_list'
                })
            }
        }
    }
</script>


