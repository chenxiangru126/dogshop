
<template>

      <div class="dialog_layer" >
        <div class="layer_cont_1 cont_1_alert">
            <div class="p-b p-t-2">
            <!-- <div class="layer_title"></div> -->
                <div class="c6 font-3 w t-c over-h p-l p-r">
                    <div style="display: flex;margin-bottom: 1.5rem;margin-top: .5rem;justify-content: center;align-items: center;"><span :style="typeN?'color: #9E9E9E;':''">购买商品</span> <input style="height: 0.1rem; line-height: 0.1rem;margin-right: .8rem;" class="switch switch-anim" type="checkbox" @click="check"> <span :style="typeN?'':'color: #9E9E9E;'"> 购买版权</span></div>
                    <div v-if="!typeN" style="display: flex;justify-content: center;align-items: center;">
                        <span @click="reduction" style="color: #548FD7;"> - </span> 
                        <span style="display: inline-block; font-size: 1.2rem;color: #FFFFFF; width:4.333333rem;height: 1.733333rem;text-align: center; background: #424242;border-radius: .733333rem;margin: 0 1.4rem">{{num}}</span> 
                        <span @click="addnum" style="color: #548FD7;">+</span>
                    </div>
                </div>
            </div>
            <div class="layer_cont_btn">
                <div class="layer_cont_confirm flex-h flex-j-c">
                    <p class='ui_cancel' @click="cancel">取  消</p>
                    <p class='ui_yes' @click="determine">确  认</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

 export default {

 data () {
    return {
       typeN:false,
      }
    },
     props: ['num'],
    created() {
         
        },
    methods: {
       reduction(){
           if(this.$parent.number>1)this.$parent.number--;
       },
       addnum(){
           if(this.$parent.number<this.$parent.goodsInfo.count){
               this.$parent.number++;
           }else{
               this.Toast('已达到库存数量上限');
           }
       },
       cancel(){
            this.$parent.dialog = false;
       },
       determine(){
            this.$parent.Place_order(this.typeN);
       },
       check(){
           this.typeN = !this.typeN;
           
       }
    }
 }
</script>
<style>
.switch {
    width: 57px;
    height: 4px;
    position: relative;
    border: 1px solid #9B9B9B;
    background-color: #9B9B9B;
    box-shadow: #9B9B9B 0 0 0 0 inset;
    border-radius: 20px;
    background-clip: content-box;
    display: inline-block;
    -webkit-appearance: none;
    user-select: none;
    outline: none;
}
.switch:before {
    content: '';
    width: 22px;
    height: 22px;
    position: absolute;
    top: -10px;
    left: -2px;
    border-radius: 20px;
    background-color:#4A8ADA;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.4);
}
.switch:checked {
    border-color:#9B9B9B;
    box-shadow: #9B9B9B 0 0 0 16px inset;
    background-color: #9B9B9B;
}
.switch:checked:before {
    left: 34px;
}
.switch.switch-anim {
    transition: border cubic-bezier(0, 0, 0, 1) 0.4s, box-shadow cubic-bezier(0, 0, 0, 1) 0.4s;
}
.switch.switch-anim:before {
    transition: left 0.3s;
}
.switch.switch-anim:checked {
    box-shadow:#9B9B9B 0 0 0 16px inset;
    background-color: #9B9B9B;
    transition: border ease 0.4s, box-shadow ease 0.4s, background-color ease 1.2s;
}
.switch.switch-anim:checked:before {
    transition: left 0.3s;
}

</style>


