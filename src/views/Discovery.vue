<template>
    <div class="full-height">
  <panel header="我的博客" :footer="footer" :list="list" :type="type"></panel>
  </div>
</template>

<script>
    import { mapMutations } from 'vuex'
    import { getBlog } from '@/api/getBlog'
   import {Panel} from 'vux'
    
    export default {
        components:{
            Panel,
        },

        data(){
            return {
                type:'1',
                list: [],
                footer: {
                    title: '查看更多',
                    url: 'http://www.jianshu.com/u/64467c788eb7'
                }
            }
        },

        created(){
            getBlog().then((res)=>{
                this.list = res.data
            })
        },

        mounted() {
            this.SET_HEADER({title:this.$t('Discovery')})
        },

        methods: {
            ...mapMutations(['SET_HEADER'])
        }
    }
</script>
