#小程序生成二维码

## 创建qrCode
> 本地新建一个qrCode.js,复制我的qrCode.js，保存

## 引入qrCode
> 在需要生成的二维码页面的小程序js里面顶部引入`let qrCode=('../../utils/qrCode.js')`
`console.log(qrCode)` 如果可以直接输出一个`api`的对象即为引入成功

## 配置参数
### wxml
> `<canvas style="width: 686rpx;height: 686rpx;background:#f1f1f1;" canvas-id="qrcCanvas"/>`
`<input value='{{qrcStr}}'  bindblur="onQrcStrBlur" type="text" maxlength="255"   
          />`
### js
> 
```
data:{
    qrStr:'xxx'  需要生成字段
    canvasId: "qrcCanvas",//需要绘画的元素
 }
 
 //适配不同屏幕大小的canvas  
   setCanvasSize:function(){  
     var size={};  
     try {  
         var res = wx.getSystemInfoSync();  
         var scale = 750/686;//不同屏幕下canvas的适配比例；设计稿是750宽  
         var width = res.windowWidth/scale;  
         var height = width;//canvas画布为正方形  
         size.w = width;  
         size.h = height;  
       } catch (e) {  
         // Do something when catch error  
         console.log("获取设备信息失败"+e);  
       }   
     return size;  
   } ,  
   
   createQrCode:function(str,canvasId,cavW,cavH){  
       //调用插件中的draw方法，绘制二维码图片  
       qrCode.api.draw(str,canvasId,cavW,cavH);  
     
    },  
     
   //获取input输入的值  
   onQrcStrBlur: function(e) {  
       this.setData({qrcStr: e.detail.value});  
   },  
     
   //在  onReady调用
   onReady: function() {  
       let size = this.setCanvasSize();//动态设置画布大小  
       this.createQrCode(this.data.qrcStr, this.canvasId, size.w, size.h);  
    },    
 ```
 
