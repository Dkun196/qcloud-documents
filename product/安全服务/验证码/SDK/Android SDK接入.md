## 前提条件
### 准备 AppId
验证码接入前，需要先在 [验证码控制台](https://console.cloud.tencent.com/captcha) 中注册获取 AppId 和 AppSecret。
### SDK 包介绍和运行环境
- 单击 [下载 Android SDK]()。
- SDK 工具包目录结构说明：
```
.
├── sdk                # captchasdk-release-1.0.2.aar
└── CaptchaDemo        # 示例工程,演示了如何使用captchasdk-release-1.0.2.aar
```
本 SDK 运行环境与项目要求：适用于 Android4.0 及以上的系统版本。

## 接入步骤
本 SDK 提供两种使用方式，分别是验证码 Dialog 和验证码 Activity。
### 方法1：使用验证码 Dialog
1. 创建一个验证码 dialog。
```
/**
 @param context，上下文
 @param appid，业务申请接入验证码时分配的appid
 @param listener，验证码验证结果回调
 @param jsonString，业务自定义参数
*/
TCaptchaDialog dialog = new TCaptchaDialog(context, appid, listener, jsonString);
```
2. 显示验证码。
```
dialog.show();
```
其中 jsonString 是 json 字符串，可以为 null。
```
JSONObject jsonObject = new JSONObject();
jsonObject.put("uin", Integer.parseInt(uin));
jsonString = URLEncoder.encode(jsonObject.toString(), "utf-8");
```
其中 listener 是根据回调返回的 json 对象值判断是否验证成功。
```
/**
json对象值：jsonObject.getInt("ret")
*/
TCaptchaVerifyListener listener = new TCaptchaVerifyListener() {
    @Override
    public void onVerifyCallback(JSONObject jsonObject) {
        int ret = jsonObject.getInt("ret");
        if(ret == 0) {
            //验证成功回调
            //jsonObject.getInt("ticket")为验证码票据
            //jsonObject.getString("appid")为appid
            //jsonObject.getString("randstr")为随机串
        } else if(ret == -1001) {
            //验证码首个TCaptcha.js加载错误，业务可以根据需要重试
            //jsonObject.getString("info")为错误信息
        } else {    
            //验证失败回调，一般为用户关闭验证码弹框
        }
    }
}
```

### 方法2：使用验证码 Activity
1. 创建 intent。
```
/**
 @param appid，业务申请接入验证码时分配的appid
*/
Intent intent = new Intent(this, TCaptchaPopupActivity.class);
intent.putExtra("appid", ***);
/**
用户自定义参数，可选；
-自定义参数放到intent的map字段中
JSONObject jsonObject = new JSONObject();
jsonObject.put("uin", Integer.parseInt(uin));
intent.putExtra("map", URLEncoder.encode(jsonObject.toString(), "utf-8"));
*/
startActivityForResult(intent, 1);
```
2. 传入 AppId，启动 TCaptchaPopupActivity。
```
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if(requestCode == 1 && data != null) {
        switch(resultCode) {
            case Activity.RESULT_OK: {
                JSONObject jsonObject = new JSONObject(data,getStringExtra("retJson"));
                int ret = jsonObject.getInt("ret");
                if(ret == 0) {
                    //验证成功回调，此时ret=0，
                    //jsonObject.getInt("ticket")为验证码票据
                    //jsonObject.getString("appid")为appid
                    //jsonObject.getString("randstr")为随机串
                } else if(ret == -1001) {
                    //验证码收个TCaptcha.js加载错误，业务可以根据需要重试
                    //jsonObject.getString("info")为错误信息
                } else {    
                    //验证失败回调，一般为用户关闭验证码弹框
                }
                break;
            }
            case Activity.RESULT_CANCELED: {
                //用户按了返回键，关闭验证码未验证成功
                break;
            }
            default:
                break;
        }
    }
}
```

至此，验证码客户端接入已完成，您可以继续完成 [后台 API 接入]()(有链接) 。