<template>
  <div>
      <el-table id="table" :data="dataList" border>
        <el-table-column prop='name' label="名字"></el-table-column>
        <el-table-column prop="age" label="年龄"></el-table-column>
        <el-table-column prop="sex" label="性别"></el-table-column>
        <el-table-column prop="career" label="职业"></el-table-column>
        <el-table-column prop="address" label="地址"></el-table-column>
      </el-table>
      <div style='margin-top:20px;'>
        <el-button type="success" plain @click="exportDom">导出数据</el-button>
      </div>
  </div>
</template>
<script>
import FileSaver from 'file-saver'
import XLSX from 'xlsx'
export default {
  data() {
    return {
      dataList:[{
        name:'牛二',
        age:'22',
        sex:'男',
        career:'测试',
        address:'某市某区某街道牛家屯',
      },{
        name:'张三',
        age:'33',
        sex:'男',
        career:'测试',
        address:'某市某区某街道张家庄',
      },{
        name:'李四',
        age:'44',
        sex:'男',
        career:'产品',
        address:'某市某区某街道李家村',
      },{
        name:'王五',
        age:'55',
        sex:'男',
        career:'码农',
        address:'某市某区某街道王家店',
      },{
        name:'马六',
        age:'66',
        sex:'男',
        career:'产品',
        address:'某市某区某街道马家沟',
      },{
        name:'田七',
        age:'77',
        sex:'男',
        career:'码农',
        address:'某市某区某街道田家寨',
      }]
    }
  },
  methods: {
    exportDom(){
      var wb = XLSX.utils.table_to_book(document.querySelector('#table'))//装table数据的元素
			var wbout = XLSX.write(wb, { bookType: 'xlsx', bookSST: true, type: 'array' })
			try {
			  FileSaver.saveAs(new Blob([wbout], { type: 'application/octet-stream' }), '人员信息列表.xlsx')
			} catch (e) {
        if (typeof console !== 'undefined') console.log(e, wbout) 
      }
			return wbout
    },
  }
};
</script>