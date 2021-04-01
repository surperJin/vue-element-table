<template>
    <div>
        <h3 class="tac fcblue">表 格 三</h3>
        <p class="tac">（行列对应）</p>

        <div class="m-30">
            <el-table
                :data="tablethree"
                :header-cell-style="{background:'#f7faff',color:'#606266'}"
                fit
                stripe
                border
                style="width: 100%"
            >
                <el-table-column prop="model" label="型号" align="center"/>
                <el-table-column prop="date" label="日期" align="center" min-width="130"/>
                <el-table-column label="编号" align="center">
                    <el-table-column v-for="(item,index) in numList" :key="index" :label="item" align="center">
                        <template slot-scope="scope">
                            <div slot="reference" :class="{
															grey: scope.row[`${item}-status`] === '0',
															green: scope.row[`${item}-status`] === '1',
															red: scope.row[`${item}-status`] ==='2',
															}">
                                {{scope.row[item]}}
                            </div>
                        </template>
                    </el-table-column>
                </el-table-column>
            </el-table>
        </div>
        <table-three-three></table-three-three>
    </div>
</template>

<script>
    import TableThreeThree from './TableThreeThree'
    export default {
        name: 'TableThree',
        components:{
            TableThreeThree
        },
        data(){
            return{
                tablethree: [
                    /*connectList只会列出有连接关系的点，不会输出一行所有的数据，如果能给出每一行所有数据当然是好的，只是会很冗余*/
                    /*连接关系：X1分别与3号、8号、9号关联，值分别为32.6、19.4、52.3，状态分别为1、2、1，最后是相应id*/
                    {
                        model: 'X1',
                        date: '2021-03-28',
                        connectList:[
                            '3-32.6-1-123456789',
                            '8-19.4-2-234567890',
                            '9-52.3-1-987654321',
                        ]
                    },
                    {
                        model: 'X2',
                        date: '2021-03-29',
                        connectList:[]
                    },
                    {
                        model: 'X3',
                        date: '2021-03-30',
                        connectList:[
                            '4-0-0-456789123',
                        ]
                    },
                ],
                numList: ['1','2','3','4','5','6','7','8','9','10'],        //编号list
            }
        },
        mounted() {
            this.tablethree.map(o=>{
                let obj = {};
                o.connectList.forEach(v=>{
                    let arr = v.split('-');
                    obj[`${arr[0]}`] =`${arr[1]}`;
                    obj[`${arr[0]}-status`] = `${arr[2]}`;
                    obj[`${arr[0]}-id`] = `${arr[3]}`;
                });
                Object.assign(o,obj);
                return o
            });
        },
        methods:{

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
