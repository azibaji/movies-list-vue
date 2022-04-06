<template>
    <nav aria-label="Page navigation example">
    <ul class="paginations">
        <li class="page-item">
            <a @click="onPageChange('previous')" :class="{'active': currentPage > 1 }">Perivius page</a> 
           
        </li>
        <li class="page-item">
             <a @click="onPageChange('next')" :class="{'active': currentPage < this.pages.length }">Next page</a>
        </li>
    </ul>
    
    </nav>
</template>
<script>
import _ from 'lodash'
export default {
    data:()=>({
        page:0
    }),
    props:{
        itemsCount:{
            type:Number,
            required:true
        },
        pageSize:{
            type:Number,
            required:true,
            default:10
        },
        currentPage:{
            type:Number,
            required:true
        }
    },
    created(){
        this.page= this.currentPage
    },
    computed:{
        pagesCount(){
            return Math.ceil(this.itemsCount / this.pageSize) === 1 ? null : Math.ceil(this.itemsCount / this.pageSize)
        },
        pages(){
            return _.range(1 , this.pagesCount + 1)
        }
    },
    methods:{
        onPageChange(value){
            switch(value){
                case 'previous':
                    if(this.page > 1){
                        this.page--
                    }
                    break;
                case 'next':
                    if(this.page < this.pages.length){
                        this.page ++
                    }
                    break;
            }
            this.$emit('onPageChange', this.page)
        },
    }
}
</script>
<style lang="scss" scoped>
nav{
    padding-bottom: 0px;
    .paginations{
        text-align: center;
        li{
            list-style: none;
            justify-content: center;
            align-items: center;
            display: inline-flex;
            height: 40px;
            padding-right: 30px;
            padding-left:30px;
            box-sizing: unset;
            font-weight: 700;
            font-size: 16px;
            line-height: 19px;
            color: rgba(0, 0, 0, 0.48);
            &:first-child{
                border-right: 1px solid #6A6A6A;
            }
            a{
                text-decoration: none;
            }
            .active{
                color: #318FE7;
            }
        }
    }
}

</style>