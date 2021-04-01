<template>
    <div>
        <h3 class="tac fcblue">表 格 一</h3>
        <p class="tac">（把数据分为两屏或者多屏）</p>

        <div class="m-30" style="display: flex">
            <div v-for="(item,index) in tableone" :key="index" style="width: 50%">
                <el-table
                    :data="item"
                    :header-cell-style="{background:'#f7faff',color:'#606266'}"
                    fit
                    highlight-current-row
                    stripe
                    border
                    style="width: 100%"
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
    export default {
        name: 'TableOne',
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
                        date: '2021-03-28',
                    },
                    {
                        model: 'X3',
                        status: '2',
                        date: '2021-03-29',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'X4',
                        status: '1',
                        date: '2021-03-29',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'X5',
                        status: '1',
                        date: '2021-03-29',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'Y1',
                        status: '1',
                        date: '2021-03-29',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'Y2',
                        status: '1',
                        date: '2021-03-29',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'Y3',
                        status: '1',
                        date: '2021-03-30',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'Y4',
                        status: '1',
                        date: '2021-03-30',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                    {
                        model: 'Y5',
                        status: '1',
                        date: '2021-03-30',
                        value1: '31.25637',
                        value2: '52.69687',
                        value3: '52.00866',
                        value4: '31.25644',
                        value5: '16.25566',
                    },
                ],
                tableone: []
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
            this.tableone = [arr1,arr2];
        },
        methods:{}
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
