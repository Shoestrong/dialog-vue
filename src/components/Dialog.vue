<template>
    <div class="st-dialog" transition="st-dialog" v-if="closeMask===true">
        <div class="st-dialog-container">
            <div class="st-dialog-header">
                <div class="st-dialog-title">{{title}}</div>
            </div>
            <div class="st-dialog-body">
                {{message}}
            </div>
            <div class="st-dialog-footer">
                <div class="st-dialog-alert-buttons" v-if="type==='alert'">
                    <div class="st-dialog-btn st-dialog-btn-full" @click="onConfirm">{{confirmButtonText}}</div>
                </div>
                <div class="st-dialog-confirm-buttons" v-if="type==='confirm'">
                    <div class="st-dialog-btn st-dialog-btn-left" @click="onCancel">{{cancelButtonText}}</div>
                    <div class="st-dialog-btn st-dialog-btn-right" @click="onConfirm">{{confirmButtonText}}</div>
                </div>
            </div>
        </div>
    </div>
</template>
<script type="text/javascript">
export default {
    name: 'dialog',
    data () {
        return {
            type: 'alert',
            closeMask: true
        }
    },
    methods:{
        _init(message, title, onConfirm, onCancel){
            let options = {
                title: title,
                message: message
            };
            if(typeof message === 'object'){
                options = message;
            }
            this._confirmFunc = onConfirm || options.onConfirm || function(){
                                    this.close();
                                };
            this._cancelFunc = onCancel || options.onCancel || function(){
                                    this.close();
                                };
            this.title = options.title || '';
            this.message = options.message || '默认内容信息';
            this.confirmButtonText = options.confirmButtonText || '确认';
            this.cancelButtonText = options.cancelButtonText || '取消';
        },
        _mount2(){
            let dialogElId = 'dialog';
            if(!document.querySelector('#dialog')){
                let dialogEle = document.createElement('div');
                dialogEle.setAttribute('id',dialogElId);
                document.body.appendChild(dialogEle);
            }
            this.$mount('#dialog');
        },
        alert(){
            this.type = 'alert';
            this._init.apply(this,arguments);
            this._mount2();
        },
        confirm(){
            this.type = 'confirm';
            this._init.apply(this,arguments);
            this._mount2();
        },
        close(){
            this.closeMask = false;
        },
        onConfirm(){
            this._confirmFunc();
        },
        onCancel(){
            this._cancelFunc();
        }
    }
}
</script>
<style type="text/css" scoped>
    .st-dialog{
        position: fixed;
        width: 100%;
        height: 100%;
        z-index: 999999;
        top: 0;left: 0;
        background-color: rgba(0,0,0,.5);
        transition: opacity .3s ease;
        font-size: 16px;
    }
    .st-dialog-container{
        position: absolute;
        top: 30%;
        left: 50%;
        margin-left: -125px;
        width: 250px;
        padding-top: 20px;
        background-color: #fff;
        border-radius: 4px;
        box-shadow: 0 2px 8px rgba(0,0,0,.5);
        transition: all .3s ease;
    }
    .st-dialog-title{
        font-style: 18px;
        text-align: center;
    }

    .st-dialog-body{
        line-height: 20px;
        padding: 10px 20px 20px;
        text-align: center;
    }
    .st-dialog-footer{
        height: 40px;
        border-top: 1px solid #cacaca;
    }
    .st-dialog-btn{
        line-height: 40px;
        font-size: 18px;
        text-align: center;
        cursor: pointer;
    }
    .st-dialog-btn-full{
        color: #fd553c;
    }
    .st-dialog-btn-disabled{
        color: #919191 !important;
    }
    .st-dialog-btn-left{
        width: 50%;
        float: left;
        border-right: 1px solid #cacaca;
        color: #919191;
    }
    .st-dialog-btn-right{
        color: #fd553c;
    }
    .st-dialog-transition{
        transition: all .3s ease;
    }
    .st-dialog-enter, .st-dialog-leave{
        opacity: 0;
    }
    .st-dialog-enter .st-dialog-container,
    .st-dialog-leave .st-dialog-container{
        transform: scale(1.1);
        -webkit-transform: scale(1.1);
    }
</style>
