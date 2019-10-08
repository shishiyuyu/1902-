
#Echarts使用文档
**开发环境下下载源代码版本**
1.  [echarts源码链接地址](https://echarts.baidu.com/dist/echarts.js)
2.  引入echarts.js文件
3.  开始绘制 
+ 准备一个具备高宽的 DOM 容器
```
	// 为 ECharts 准备一个具备高宽的 DOM 容器。
<div id="main" style="width: 600px;height:400px;"></div>
```
+ 通过 echarts.init 方法初始化一个 echarts 实例
```
	// 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));
```
+ 指定图表的配置项和数据**option**
```
var option = {
			// 标题
            title: {
	            // 标题文本内容
                text: 'ECharts 入门示例'
            },
            // 图例 说明、解释
            legend: {
                data:['销量']
            },
            // x轴方向的数据
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            // y轴方向的数据
            yAxis: {},
            // 系列列表
            series: [{
                name: '销量',
                // type属性定义图标类型
                type: 'bar',
                // 定义数据
                data: [5, 20, 36, 10, 10, 20],
                // 普通样式
                itemStyle: {
                    // 点的颜色。
                    color: 'green'
                },
                label: {
                    show: true,
                    // 标签的文字。
                    formatter: 'This is a normal label.'
                },
                 // 高亮样式。
                emphasis: {
                    itemStyle: {
                        // 高亮时点的颜色。
                        color: 'blue'
                    },
                    label: {
                        show: true,
                        // 高亮时标签的文字。
                        formatter: 'This is a emphasis label.'
                    }
                }
            }]
        };
```
+ 使用刚指定的配置项和数据显示图表。
```
myChart.setOption(option);
```
**ECharts 中的样式简介**
1. 颜色主题
```
	// 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'),'light OR dark');
```
2. 调色盘
3. 高亮的样式：emphasis
**作业一: 用折线图实现未来一周天气变化 **
[示例](https://img-blog.csdnimg.cn/20181101120604827.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dkamxj,size_16,color_FFFFFF,t_70)
**作业一: 用折线图实现未来一周天气变化 **


