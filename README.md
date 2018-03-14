# 前端开发学习随记
## 一、README.md 语法规则<br>
### 1.1 换行<br>
    段落1<br>段落2<br>
  段落1<br>段落2<br>
### 1.2 标题
    #一级标题  
    ##二级标题  
    ###三级标题  
    ####四级标题  
    #####五级标题  
    ######六级标题<br>
### 1.3 区块
    >区块1
    >>区块2
    >>>区块3
    >>>>区块4
  >区块1
  >>区块2
  >>>区块3
  >>>>区块4
### 1.4 列表
    注意：* + - 前后加空格，tab键或四个空格可分级）
     * 列表1
        + 列表2
            - 列表3
 * 列表1
    + 列表2
        - 列表3
### 1.5 链接
    [百度一下-你就知道](http://www.baidu.com "百度一下")
  [百度一下-你就知道](http://www.baidu.com "百度一下")
### 1.6其他
    插入代码片段：在代码上下行用```标记，注意`符号是tab键上面那个，要实现语法高亮，则在```后面加上编程语言的名称

    ```Java
    public static void main(String[] args){}
    ```
    ```javascript
    document.getElementById("ts").innerHTML="Hello"
    ```
```Java
public static void main(String[] args){}
```
```javascript
document.getElementById("ts").innerHTML="Hello"
```
    单行文本：前面使用两个Tab

    多行文本:每行行首加两个Tab

    部分文字高亮：使用``包围，这个符号不是单引号，而是Tab上方，数字1左边那个按键的符号

    文字超链接格式：[要显示的文字](链接的地址"鼠标悬停显示")，在URL之后用双引号括起来一个字符串，即鼠标悬停显示的文本，可不写
    
## 二、微信小程序关键知识点<br>
### 2.1 http
```javascript
	wx.request(OBJECT);
	例子：
	wx.request( {
		url: "http://op.juhe.cn/onebox/weather/query",
		header: {
			"Content-Type": "application/x-www-form-urlencoded"
		},
		method: "POST",
	//data: { cityname: "上海", key: "1430ec127e097e1113259c5e1be1ba70" },
		data: Util.json2Form( { cityname: "上海", key: "1430ec127e097e1113259c5e1be1ba70" }),
		complete: function( res ) {
			that.setData( {
				toastHidden: false,
				toastText: res.data.reason,
				city_name: res.data.result.data.realtime.city_name,
				date: res.data.result.data.realtime.date,
				info: res.data.result.data.realtime.weather.info,
			});
			if( res == null || res.data == null ) {
				console.error( '网络请求失败' );
				return;
			}
		}
	})
```
### 2.2 路由
```javascript
	// 一、保留当前页面，跳转到应用内的某个页面，使用wx.navigateBack可以返回到原页面。
	// 注意：目前页面路径最多只能十层。
		wx.navigateTo(OBJECT)

		// 示例1
		wx.navigateTo({
			url: 'test?id=1'
		})
		//test.js
		Page({
			onLoad: function(option){
				console.log(option.query)
			}
		})

		// 示例二
		wx.navigateTo({
		    url:"pages/home/home?type=2"
		});

		// 然后在home.js中的onLoad()函数中得到值：option.type就可以得到了，如下：

		onLoad: function (option) {
		    this.setData({
		        type:option.type,
		    });
		    console.log(option.type);
		}

	// 二、关闭当前页面，跳转到应用内的某个页面。
		wx.redirectTo(OBJECT)
		// 示例
		wx.redirectTo({
			url: 'test?id=1'
		})
		//test.js
		Page({
			onLoad: function(option){
				console.log(option.query)
			}
		})


	// wx.navigateTo()是保留当前页面，跳转到某个页面，跳转页面后可以返回上一页。
	// wx.redirectTo()是关闭当前页面，跳转到某个页面，跳转页面后不能返回上一页。

	// 等等
```
### 2.3 全局方法和数据
```javascript
        // 全局的 getApp() 函数可以用来获取到小程序实例。
        // other.js
        var appInstance = getApp()
        console.log(appInstance.globalData) // I am global data
```
## 2.4 page 内数据和方法
```javascript
	//改变数据
	this.setData({
	    message:"你好 米娜！"
	})
	//获取数据
	this.data.message

	// 调用本页方法：
	this.method();

	##其他
	// currentTarget 事件属性返回其监听器触发事件的节点，即当前处理该事件的元素、文档或窗口。
	// event.currentTarget
```
