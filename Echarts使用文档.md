
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
**作业二: 用折线图实现未来一周天气变化 **
[示例](https://images2018.cnblogs.com/blog/1150667/201803/1150667-20180302110618565-96310848.png)
**个性化图表样式**
饼图主要是通过扇形的弧度表现不同类目的数据在总和中的占比
```
var option = {
    // 全局的背景色
    backgroundColor: 'pink',
    // 全局的文字颜色
     textStyle: {
        color: 'red'
    },
    // 视觉引导线的颜色
    labelLine: {
        lineStyle: {
            color: 'rgba(255, 255, 255, 0.3)'
        }
    },
    
    series : [
        {
            name: '访问来源',
            type: 'pie',
            radius: '55%',
            // 南丁格尔图
            roseType: 'angle',
            data:[
                {value:235, name:'视频广告'},
                {value:274, name:'联盟广告'},
                {value:310, name:'邮件营销'},
                {value:335, name:'直接访问'},
                {value:400, name:'搜索引擎'}
            ],
            itemStyle: {
                 // 阴影的大小
                shadowBlur: 500,
                 // 阴影水平方向上的偏移
                shadowOffsetX: 0,
                // 阴影垂直方向上的偏移
                shadowOffsetY: 0,
                 // 阴影颜色
                shadowColor: 'rgba(0, 0, 0, 0.5)',
                // 高亮时候的样式
                emphasis: {
                    shadowBlur: 200,
                    shadowColor: 'rgba(255, 0, 0,1)'
                },
                // 设置全局扇形的颜色
                color: '#c23531',
            },
            
        }
    ]
};
myChart.setOption(option)
```
**通过设置 roseType 显示成南丁格尔图**
```
	// 南丁格尔图会通过半径表示数据的大小。
	roseType: 'angle'
```

**异步数据加载和更新示例**
```
var myChart = echarts.init(document.getElementById("main"));
var option = {
      title: {
            text: '异步数据加载示例'
      },
      tooltip: {},
      legend: {
            data:['销量']
      },
      xAxis: {
            data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
      },
      yAxis: {},
      series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
      }]
}
myChart.showLoading();
$.ajax({
      url: "1.json",
      type: "get",
      success: function(data) {
            if(data.result == 'OK') {
                  option.xAxis.data = [];
                  option.series[0].data = [];
                  var arr = data.data
                  $.each(arr,function(item,index){
                        option.xAxis.data.push(index.title);
                        option.series[0].data.push(index.num);
                  })
                  setTimeout(function(){
                        myChart.hideLoading();
                        myChart.setOption(option);
                  },3000)
                  
            }
      }
})
```