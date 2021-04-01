<template>
    <div>
        <p class="tac">（多屏表格单元格点击事件）</p>
        <div class="m-30" style="display: flex">
            <div v-for="(item,index) in tabletwo" :key="index" style="width: 50%">
                <el-table
                    :data="item"
                    :header-cell-style="{background:'#f7faff',color:'#606266'}"
                    @cell-click="cellClickHandle(index,arguments)"
                    :cell-class-name="tableCellClassName"
                    fit
                    stripe
                    border
                    style="width: 100%"
                    class="pointer"
                >
                    <el-table-column prop="model" label="机型" align="center"/>
                    <el-table-column
                        label="状态"
                        align="center"
                    >
                        <template slot-scope="scope">
                        <span :class="{grey :scope.row.status === '0',green :scope.row.status === '1',red :scope.row.status === '2'}">
                            {{ scope.row.statusTxt }}
                        </span>
                        </template>
                    </el-table-column>
                    <el-table-column prop="date" label="日期" align="center" min-width="130"/>
                    <el-table-column prop="value1" label="数值1" align="center"/>
                    <el-table-column prop="value2" label="数值2" align="center"/>
                    <el-table-column prop="value3" label="数值3" align="center"/>
                    <el-table-column prop="value4" label="数值4" align="center"/>
                    <el-table-column prop="value5" label="数值5" align="center"/>
                </el-table>
            </div>
        </div>
    </div>
</template>

<script>
    function Foo(val,data) {
        const obj = {
            0: data.model,
            1: data.statusTxt,
            2: data.date,
            3: data.value1,
            4: data.value2,
            5: data.value3,
            6: data.value4,
            7: data.value5,
        };
        var valTxt;
        valTxt = obj[val] || '';
        if (valTxt != '--'){
            alert(valTxt)
        }
    }
    export default {
        name: 'TableTwoTwo',
        data(){
            return{
                listData: [
                    {
                        model: 'X1',
                        status: '1',
                        date: '2021-03-28',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'X2',
                        status: '0',
                        date: '2021-03-29',
                    },
                    {
                        model: 'X3',
                        status: '2',
                        date: '2021-03-30',
                        value1: '8.25637',
                        value2: '97.69687',
                        value3: '78.00866',
                        value4: '12.25644',
                        value5: '4.25566',
                    },
                    {
                        model: 'X4',
                        status: '1',
                        date: '2021-03-31',
                        value1: '1.25637',
                        value2: '0.69687',
                        value3: '33.00866',
                        value4: '45.25644',
                        value5: '23.25566',
                    },
                ],
                tabletwo: []
            }
        },
        mounted() {
            var arr1=[];var arr2=[];
            this.listData.map((o,index)=>{
                const obj = {
                    0: '已废弃',
                    1: '运行中',
                    2: '故障'
                };
                o.statusTxt = obj[o.status] || '';
                /*保留小数后一位*/
                o.value1 ? o.value1 = Number(o.value1).toFixed(1) : o.value1 = '--';
                o.value2 ? o.value2 = Number(o.value2).toFixed(1) : o.value2 = '--';
                o.value3 ? o.value3 = Number(o.value3).toFixed(1) : o.value3 = '--';
                o.value4 ? o.value4 = Number(o.value4).toFixed(1) : o.value4 = '--';
                o.value5 ? o.value5 = Number(o.value5).toFixed(1) : o.value5 = '--';
                if (index < this.listData.length / 2) {
                    arr1.push(o)
                }else {
                    arr2.push(o)
                }
            });
            this.tabletwo = [arr1,arr2];
        },
        methods:{
            tableCellClassName({row, column, rowIndex, columnIndex}){//注意这里是解构
                //利用单元格的 className 的回调方法，给行列索引赋值
                row.index=rowIndex;
                column.index=columnIndex;
            },
            /*点击单元格*/
            cellClickHandle(index,val){
                var list;
                if (index === 0) {
                    list = this.tabletwo[0]
                }else {
                    list = this.tabletwo[1]
                }
                console.log(val[0].index);      //行row
                console.log(val[1].index);      //列column
                for (let i = 0; i < list.length; i++) {
                    if (val[0].index === i) {
                        Foo(val[1].index,list[i])
                    }
                }
            },
        }
    }
</script>

<style scoped>
    .grey{
        color: #a3a3a3;
    }
    .green{
        color: #2ecc0f;
    }
    .red{
        color: #ff371e;
    }
</style>
