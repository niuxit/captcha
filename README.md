# captcha
## 牛X验证
> 简介：完全免费+不限调用量+验证行为的人机验证，采用旋转图片的方式，让你可以轻松的完成验证，让识别验证的成本更高，让你的业务更安全。
### 特点：
1. 完全免费
2. 不限调用量
3. 兼容所有主流浏览器和各个平台
4. js SDK调用简单，无学习成本
5. 分级验证，对可疑用户要求更严格
6. 多种使用形式，可无缝更新到你的业务
### 前端调用
1. 引入js，
`<script src="https://cdn.jsdelivr.net/gh/niuxit/captcha@{version}/captcha.min.js"></script>`
{version}为最新的版本
2. 实例化验证类，参数如下
 
|   参数  |  参数类型   |   必填   |默认|说明|
| ---- | --- | --- |--- |--- |
|appid|  string   |   是   |无|你申请到的appid|
|style|  string   |   是   |无|验证码样式，包含3种:`"float"`（触发式）、`"embed"`（嵌入式）、`"popup"`（弹出式）|
|element|  string   |   是   |无|验证码容器，如:`"#captcha"`|
|onload|  function   |   否   |无|验证码必须文件加载完毕时触发|
|callback|  function   |   否   |无|验证码验证状态回调,具体看完整示例|
|state|  string|   否   |根据验证形式不同|是否显示状态栏,形式为`"float"`时固定为1(显示)，`"popup"`时默认为0(不显示),`"embed"`时默认为1|
|cancle|  boolean|   否   |`true`|是否可取消验证码|
|lang|  string|   否   |`"auto"`|语言，默认为自动(根据用户浏览器变化语言)，目前支持5种语言，分别为：`cn`(简体中文)，`tw`(繁体中文),`en`(英文),`ja`(日语),`ko`(韩语)|
|text|  string|   否   |`"请完成人机验证"`|状态栏提示语，如果自定义则不会根据语言变化|
|alt|  string|   否   |`"牛X验证"`|logo提示语|
|logo|  string|   否   |默认logo|logo地址，如：`"//test.com/logo.png"`|
3. 方法：

|  方法名   |   参数  | 说明  |
| --- | --- |--- |
|  show  |   refresh  | 显示验证码，默认refresh=0，=1时强制刷新验证码，用于同一页面需要多次验证的情况  |
|  hide|   无| 隐藏验证码，隐藏后仍然可再次调用show显示验证码  |
|  reset|   无| 重置证码，用于在验证成功之后再次发起验证的情景(`obj.show(1)`即可达到重置+显示的效果)|
|  destory|   无| 销毁验证码，销毁后不可再次调用对象的任何方法  |
4. 完整示例：
```
<script src="https://cdn.jsdelivr.net/gh/niuxit/captcha@1.2.4/captcha.min.js"></script>
var captcha=new niux_captcha({
    appid:"**********************************",
    style:"embed",
    element:"#float_test",
    callback:function (data) {
        /*data={
            ret:1,//为1时为验证成功，0为验证失败
            captcha_sig:"xxxxxxxxxxxxxx",//用于后端进行二次校验的sig，
        }*/
        if(data.ret==1){
            //验证成功
            //你的业务逻辑
            location.href="server.php?captcha_sig="+data.captcha_sig;

        }else if(data.ret==0){
            //用户取消验证
            alert("请完成验证！");
        }
    },
    onload:function(){
        //验证码初始化完成
        //this.show(1);
    },
    state:1,//显示状态栏
    cancel:0,//不可被取消
    lang:"auto",//语言为自动
    logo:"",//使用默认loho
    alt:"",//使用默认logo提示语
    text:"请完成验证",//状态栏提示语
});
```


