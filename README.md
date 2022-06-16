# SpreadJS_HighlightMatch
搜索时单元格匹配内容高亮显示
### SpreadJS 示例，基于 JavaScript组件实现高亮搜索效果

该示例包括使用 SpreadJS API 的演示脚本，可用于实现包含合并单元格的数据绑定。
有关 SpreadJS API 的更多信息，请参阅[SpreadJS API指南]( https://demo.grapecity.com.cn/spreadjs/help/api/) 和[帮助手册]( https://help.grapecity.com.cn/pages/viewpage.action?pageId=5963808)。
 

目录：
运行步骤
控件初始化
示例代码
关于 SpreadJS
外部文件：
临时授权申请



运行步骤
1. 在开始之前，请确保您已满足以下先决条件：

要运行 SpreadJS，浏览器必须支持 HTML5，客户端导入和导出 Excel 需要 IE10及以上。请先了解 SpreadJS 的产品使用环境，并申请临时部署授权激活
安装并更新NodeJS和NPM
2. 克隆或下载此代码库
3. 初始化控件，并运行示例脚本

控件初始化
1. 首先，创建一个新页面，并在页面上输入以下代码：
<!DOCTYPE html>
    <html>
    <head>
        <title>Spread HTML test page</title>

2. 在页面中添加对 Spread.JS 的引用。代码如下。需要注意的是，Spread 提供压缩过（minified）的 JavaScript 文件和和用于调试的文件：
<script src="[Your_Scripts_Path]/gc.spread.sheets.all.xxxx.min.js" type="text/javascript"></script>

3. 添加 CSS 文件以改变Spread.JS 的外观。默认的CSS文件名为： gc.spread.sheets.xxxx.css，里面包含了所有的默认样式。该 CSS 文件将会影响滚动条，筛选框及其子元素，单元格和下方标签栏的样式。引入 CSS 的代码如下：
//<link href="[Your_CSS_Path]/gc.spread.sheets.xxxx.css" rel="stylesheet" type="text/css"/>
//OR
<link href="[Your_CSS_Path]/bootstrap/bootstrap.min.css" rel="stylesheet" type="text/css"/>
<link href="[Your_CSS_Path]/bootstrap/bootstrap-theme.min.css" rel="stylesheet" type="text/css"/>

4. 添加产品授权，代码为：
GC.Spread.Sheets.LicenseKey = "xxx";

5. 添加控件初始化代码。本例会在一个 id 为“ss”的 DOM 元素上初始化 Spread.Sheets：
<script type="text/javascript">
// Add your license
 GC.Spread.Sheets.LicenseKey = "xxx";
// Add your code
 window.onload = function(){
var spread = new GC.Spread.Sheets.Workbook(document.getElementById("ss"),{sheetCount:3});
var sheet = spread.getActiveSheet();
 }
</script>
</head>
<body>

6. 创建一个 id 为 “ss”的元素，Spread.Sheets 将在该 DOM 中初始化：
<div id="ss" style="height: 500px; width: 800px"></div>
</body>
</html>

示例代码
```
HTML：
    <p>高亮搜索效果</p>
    <div id='log'>
        <label>输入搜索内容:</label>
        <input id="searchTxt" type="text" />
    </div>
    <div id='ss'></div>
CSS：
    #ss {
        height: 400px;
        width: 100%
    }
    p{
        text-align: center;
        color: #336699;
    }
    #log{
        margin-bottom: 10px;
    }
JavaScript：
    var spreadNS = GC.Spread.Sheets;
    window.onload = function() {
        function getDataSource() {
            var source = [{
                LastName: "张伟",
                FirstName: "Nancy",
                Title: "Sales Representative",
                Phone: "(123)555-0100",
                Email: "nancy@northwindtraders.com"
            }, {
                LastName: "王伟",
                FirstName: "Andrew",
                Title: "Vice President, Sales",
                Phone: "(123)555-0100",
                Email: "andrew@northwindtraders.com"
            }, {
                LastName: "王芳",
                FirstName: "Jan",
                Title: "Sales Representative",
                Phone: "(123)555-0100",
                Email: "jan@northwindtraders.com"
            }, {
                LastName: "李娜",
                FirstName: "Mariya",
                Title: "Sales Representative",
                Phone: "(123)555-0100",
                Email: "mariya@northwindtraders.com"
            }, {
                LastName: "王静",
                FirstName: "Steven",
                Title: "Sales Manager",
                Phone: "(123)555-0100",
                Email: "steven@northwindtraders.com"
            }, {
                LastName: "刘伟",
                FirstName: "Michael",
                Title: "Sales Representative",
                Phone: "(123)555-0100",
                Email: "michael@northwindtraders.com"
            }, {
                LastName: "王秀英",
                FirstName: "Robert",
                Title: "Sales Representative",
                Phone: "(123)555-0100",
                Email: "robert@northwindtraders.com"
            }, {
                LastName: "李化民",
                FirstName: "Laura",
                Title: "Sales Coordinator",
                Phone: "(123)555-0100",
                Email: "laura@northwindtraders.com"
            }, {
                LastName: "李庆华",
                FirstName: "Susan",
                Title: "Sales Representative",
                Phone: "(123)555-0100",
                Email: "anne@northwindtraders.com"
            }];
            return source;
        }
        var columnInfo = [{
                name: "LastName",
                displayName: "中文名",
                cellType: new HighlightSearchCellType(),
                size: 80
            }, {
                name: "FirstName",
                displayName: "英文名",
                cellType: new HighlightSearchCellType(),
                size: 80
            }, {
                name: "Phone",
                displayName: "电话",
                cellType: new HighlightSearchCellType(),
                size: 180
            }, {
                name: "Email",
                displayName: "邮箱",
                cellType: new HighlightSearchCellType(),
                size: 200
            },
    
        ];
        var spread = new GC.Spread.Sheets.Workbook(document.getElementById("ss"));
        var sheet = spread.getActiveSheet();
        spread.isPaintSuspended(true);
        sheet.setDataSource(getDataSource());
        sheet.bindColumns(columnInfo);
        // 定义自定义单元格
        var style = new GC.Spread.Sheets.Style();
        spread.isPaintSuspended(false);
        document.getElementById("searchTxt").onkeyup = (function() {
            sheet.searchText = document.getElementById("searchTxt").value;
            spread.repaint();
        });
    };
    
    function HighlightSearchCellType() {}
    HighlightSearchCellType.prototype = new GC.Spread.Sheets.CellTypes.Text();
    HighlightSearchCellType.prototype._generateSearchBlock = function(text, search) {
        if (text === "" || text === null || text === undefined || search === "" || search === null || search === undefined) {
            return null;
        }
        var originalText = text.toLowerCase();
        var searchText = search.toLowerCase();
        var patt = new RegExp(searchText, "g");
        var result, blocks = [],
            start = 0,
            end = 0,
            subStr = "";
        while ((result = patt.exec(originalText)) != null) {
            end = patt.lastIndex - searchText.length;
            if (start < end) {
                //normal block
                blocks.push({
                    start: start,
                    end: end,
                    text: text.substring(start, end),
                    highlight: false
                });
            }
            //highlight block
            start = end;
            end = patt.lastIndex;
            blocks.push({
                start: start,
                end: end,
                text: subStr = text.substring(start, end),
                highlight: true
            });
            start = end;
        }
        if (start === 0) {
            return null;
        }
        //the last block
        if (end < originalText.length) {
            blocks.push({
                start: end,
                end: end + subStr.length,
                text: text.substring(end),
                highlight: false
            });
        }
        return blocks;
    }
    HighlightSearchCellType.prototype.paintValue = function(ctx, value, x, y, w, h, style, options) {
        var text = this.format(value, style.formatter);
        if (!text) {
            return;
        }
        ctx.save();
        ctx.rect(x, y, w, h);
        ctx.clip();
        ctx.beginPath();
        ctx.textAlign = "left";
        ctx.textBaseline = "alphabetic";
    
        if (style.font) {
            ctx.font = style.font;
        }
        if (style.foreColor) {
            ctx.fillStyle = style.foreColor;
        }
        var originalStyle = ctx.fillStyle;
        var fontSize = options.fontInfo.fontSize;
        var lineHeight = options.lineHeight;
        var baselineOffset = fontSize > 8 ? Math.floor((fontSize - 8) / 5 + 2) : 1;
        var lineOffset = lineHeight / 2 - fontSize / 2 + baselineOffset;
        var adjY = lineHeight - lineOffset + 2;
        var blocks = this._generateSearchBlock(text, options.sheet.searchText);
        if (blocks) {
            for (var i = 0; i < blocks.length; i++) {
                var block = blocks[i];
                if (block.highlight) {
                    ctx.fillStyle = "red";
                } else {
                    ctx.fillStyle = originalStyle;
                }
                ctx.fillText(block.text, x + 2, y + adjY);
                x += ctx.measureText(block.text).width;
            }
        } else {
            ctx.fillText(text, x + 2, y + adjY);
        }
    
        ctx.restore();
}
```
#### 关于 SpreadJS
[SpreadJS]( https://www.grapecity.com.cn/developer/spreadjs) 是一款基于 HTML5 的纯前端表格控件，兼容 450 多种 Excel 公式，具备“高性能、跨平台、与 Excel 高度兼容”的产品特性。使用 SpreadJS，可直接在 Angular、 React、 Vue 等前端框架中实现高效的模板设计、在线编辑和数据绑定等功能，为最终用户提供高度类似 Excel 的使用体验。
 

