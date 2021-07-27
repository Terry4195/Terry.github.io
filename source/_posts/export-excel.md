---
title: web导出excel
date: 2021-06-11 15:31:50
tags: ["javascript"]
index_img: https://qiniu.zhaoxinchuan.cn/excel/excel.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
---

### web 端导出 table 中的数据，将数据导出为 excel 文件是后台管理系统中常见的需求，导出的方法也有很多中，下面给出几个常用的方法

1. 使用 table 标签的形式导出

```html
<html>
  <head> </head>
  <body class="body">
    <script>
      //要导出的json数据
      const jsonData = [
        {
          name: "路人甲",
          phone: "123456",
          email: "123@123456.com",
        },
        {
          name: "路人乙",
          phone: "123456",
          email: "123@123456.com",
        },
        {
          name: "路人丙",
          phone: "123456",
          email: "123@123456.com",
        },
      ];
      //列标题
      let str = "<tr><td>姓名</td><td>电话</td><td>邮箱</td></tr>";
      //循环遍历，每行加入tr标签，每个单元格加td标签
      for (let i = 0; i < jsonData.length; i++) {
        str += "<tr>";
        for (let item in jsonData[i]) {
          //增加\t为了不让表格显示科学计数法或者其他格式
          str += `<td>${jsonData[i][item] + "\t"}</td>`;
        }
        str += "</tr>";
      }

      //Worksheet名
      let worksheet = "Sheet1";
      let uri = "data:application/vnd.ms-excel;base64,";

      //下载的表格模板数据
      let templates = `<table>${str}</table><p style='font-size: 20px;color: red;'>使用table标签方式将json导出xls文件</p><button onclick='tableToExcel()'>导出</button>`;
      //下载模板
      let body = document.getElementsByClassName("body")[0];
      body.innerHTML = templates;
      function tableToExcel() {
        var template = `${templates}</head><body></body></html>`;
        window.location.href = uri + base64(template);
      }
      //输出base64编码
      function base64(s) {
        return window.btoa(unescape(encodeURIComponent(s)));
      }
    </script>
  </body>
</html>
```

2. jquery + jquery-table2excel

   > 插件地址：[jquery-table2excel](https://github.com/rainabba/jquery-table2excel)

   ```html
   <body>
     <table id="table" border="1" cellspacing="0" width="100%">
       <thead>
         <tr>
           <th>姓名</th>
           <th>年龄</th>
           <th>邮箱</th>
         </tr>
       </thead>
       <tbody>
         <tr>
           <td>路人甲</td>
           <td>18</td>
           <td>18@163.com</td>
         </tr>
       </tbody>
     </table>
     <button class="btn">导出excel表格</button>
     <script src="https://cdn.bootcdn.net/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
     <script src="./js/jquery.table2excel.js"></script>
     <script>
       // 配置
       // exclude： 不被导出的表格行的CSS class类。
       // name： 导出的Excel文档的名称。
       // filename： Excel文件的名称。
       // fileext: 文件后缀名
       // exclude_img： 是否导出图片。
       // exclude_links： 是否导出超链接
       // exclude_inputs： 是否导出输入框中的内容。
       $(".btn").click(() => {
         $("#table").table2excel({
           filename: "导出excel",
         });
       });
     </script>
   </body>
   ```

3. [xlxs.js](https://github.com/SheetJS/sheetjs/blob/master/dist/xlsx.js)
