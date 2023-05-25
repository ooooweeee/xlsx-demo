<template>
  <div class="app">This is App</div>
  <input type="file" @change="readWorkbookFromLocalFile" name="" id="" />
</template>

<script>
import { defineComponent } from 'vue';
import * as XLSX from 'xlsx';

export default defineComponent({
  setup() {
    function readWorkbookFromLocalFile(event) {
      var reader = new FileReader();
      reader.onload = function (e) {
        var data = e.target.result;
        // 读取二进制的excel
        var workbook = XLSX.read(data, { type: 'binary' });
        const sheetName = workbook.SheetNames[0]; //获取数据的表名
        const sheet = workbook.Sheets[sheetName]; //workSheet 是该excel表格中的数据
        const jsonData = XLSX.utils.sheet_to_json(sheet); //数据解析,输出JSON格式
        console.log(jsonData);
      };
      reader.readAsBinaryString(event.target.files[0]);
    }

    return {
      readWorkbookFromLocalFile
    };
  }
});
</script>
