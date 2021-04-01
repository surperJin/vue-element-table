<template>
    <div>
        <p class="tac">（动态多级表头行列对应）</p>

        <div class="m-30">
            <el-table
                :data="tableThree"
                fit
                stripe
                border
                style="width: 100%"
            >
                <el-table-column prop="model" label="型号" align="center" fixed/>
                <el-table-column prop="date" label="日期" align="center" min-width="130"/>
                <el-table-column v-for="(item,index) in headerList" :key="index" :label="item.name" align="center">
                    <el-table-column :label="item.code" align="center">
                        <el-table-column v-for="(items,indexs) in item.typenum" :key="indexs" :label="items" align="center" width="60">
                            <template slot-scope="scope">
                                <div slot="reference"
                                     :class="{
											grey: scope.row[`${item.code}-${items}-status`] ==='0'	,
											green: scope.row[`${item.code}-${items}-status`] ==='1',
											red: scope.row[`${item.code}-${items}-status`] ==='2'	,
										}"
                                >
                                    {{scope.row[`${item.code}-${items}`]}}
                                </div>
                            </template>
                        </el-table-column>
                    </el-table-column>
                </el-table-column>
            </el-table>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'TableThreeThree',
        data(){
            return{
                headerList: [
                    {
                        name: '类别1',
                        code: 'K01',
                        typenum: ['1','2','3','4']
                    },
                    {
                        name: '类别2',
                        code: 'K02',
                        typenum: ['1','2']
                    },
                    {
                        name: '类别3',
                        code: 'K03',
                        typenum: ['1','2','3']
                    },
                    {
                        name: '类别4',
                        code: 'K04',
                        typenum: ['1','2','3','4']
                    },
                    {
                        name: '类别5',
                        code: 'K05',
                        typenum: ['1','2','3','4']
                    },
                    {
                        name: '类别6',
                        code: 'K06',
                        typenum: ['1','2','3','4','5','6']
                    },
                ],
                tableThree: [
                    {
                        connectList: [],
                        model: 'X1',
                        num: '1',
                        date: '2021-03-30'
                    },
                    {
                        /*连接关系：X2与K02的2号相关联，值为46.2，状态为1，最后为相应id*/
                        connectList: ['K02-2-46.2-1-0123456789'],
                        model: 'X2',
                        num: '2',
                        date: '2021-03-30'
                    },
                    {
                        connectList: [],
                        model: 'X3',
                        num: '3',
                        date: '2021-03-31'
                    },
                    {
                        connectList: ['K01-3-10.3-1-1234567890','K04-4-15.6-2-2345678901'],
                        model: 'X4',
                        num: '1',
                        date: '2021-04-01'
                    },
                    {
                        connectList: ['K03-1-0-0-3456789012'],
                        model: 'X5',
                        num: '2',
                        date: '2021-04-01'
                    },
                    {
                        connectList: [],
                        model: 'X6',
                        num: '1',
                        date: '2021-04-01'
                    },
                    {
                        connectList: [],
                        model: 'X7',
                        num: '2',
                        date: '2021-04-01'
                    },
                    {
                        connectList: ['K04-1-32.2-1-5678901234'],
                        model: 'X8',
                        num: '3',
                        date: '2021-04-01'
                    },
                ]
            }
        },
        mounted() {
            this.tableThree.map(o=>{
                let obj = {};
                o.linkId = [];
                o.connectList.forEach(v=>{
                    let arr = v.split('-');
                    obj[`${arr[0]}-${arr[1]}`] = arr[2];
                    obj[`${arr[0]}-${arr[1]}-status`] = arr[3];
                    obj[`${arr[0]}-${arr[1]}-id`] = arr[4];
                    o.linkId.push(arr[4]);
                    Object.assign(o,obj)
                })
            });
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
