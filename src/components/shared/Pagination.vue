<template>
    <nav aria-label="Page navigation example">
    <ul class="paginations">
        <li class="page-item" :class="{'active': currentPage === page }" v-for="page in pages" :key="page">
                <a @click="onPageChange(page)" v-if="page === 1" :class="{'active': currentPage > 1 }">Perivius page</a> 
                <a @click="onPageChange(page)" v-if="page === 2" :class="{'active': currentPage < 2 }">Next page</a>
        </li>
    </ul>
    
    </nav>
</template>
<script>
import _ from 'lodash'
export default {
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
    computed:{
        pagesCount(){
            return Math.ceil(this.itemsCount / this.pageSize) === 1 ? null : Math.ceil(this.itemsCount / this.pageSize)
        },
        pages(){
            return _.range(1 , this.pagesCount + 1)
        }
    },
    methods:{
        onPageChange(page){
            this.$emit('onPageChange', page)
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