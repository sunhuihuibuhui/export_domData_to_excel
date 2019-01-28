<template>
<!-- 进出管理 -->
  <div>
    <el-button type="success" plain icon="el-icon-upload2" @click="exportExcel">导出</el-button>
    <div>
      <el-table id="table" :data="dataList" border>
        <el-table-column prop='name' label="名字"></el-table-column>
        <el-table-column prop="age" label="年龄"></el-table-column>
        <el-table-column prop="sex" label="性别"></el-table-column>
        <el-table-column prop="career" label="职业"></el-table-column>
        <el-table-column prop="address" label="地址"></el-table-column>
        <el-table-column prop="ID" label="身份证号"></el-table-column>
      </el-table>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      dataList:[{
        name:'张三',
        age:'33',
        sex:'男',
        career:'测试',
        address:'某市某区某街道张家庄',
        ID:'1234567890987654321'
      },{
        name:'李四',
        age:'44',
        sex:'男',
        career:'产品',
        address:'某市某区某街道李家村',
        ID:'1234567890987654321'
      },{
        name:'王五',
        age:'55',
        sex:'男',
        career:'码农',
        address:'某市某区某街道王家店',
        ID:'1234567890987654321'
      }]
    }
  },
  methods: {
    exportExcel(){
      const { export_json_to_excel } = require('../../static/js/Export2Excel')  //这里必须使用绝对路径
      const tHeader = ['姓名', '年龄', '职业', '性别', '住址']  //表头
      const filterVal = ['name', 'age', 'career', 'sex','address']  //表头对应的数据字段
      const list = this.dataList;//要导出的数据list
      const data = this.formatJson(filterVal, list);
      const title = '信息列表';
      export_json_to_excel(tHeader, data, title); // 导出的表格名称，根据需要自己命名
		},	
		formatJson(filterVal, jsonData){
			return jsonData.map(v =>{
				return filterVal.map(j => v[j])
			})
		},
  }
};
</script>