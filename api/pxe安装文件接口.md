# pxe安装文件接口

## 请求地址

名称 | 说明
--- | ---
请求地址 | http://localhost:8083/api/osinstall/v1/report/deviceMacInfo
编码 | UTF-8
请求方式 | POST
请求参数格式 | application/json

## 请求参数

字段 | 类型 | 是否必填 | 描述
--- | --- | --- | ---
Sn | string | 是 | SN序列号
Mac | string | 是 | MAC地址

## 请求参数示例

```json
{
  "Sn": "test",
  "Mac": "EA:1F:2d:3a:4H"
}
```	
## 请求示例（PHP）

```php
<?php
$data = array("Sn" => "test","Mac" => "EA:1F:2d:3a:4H");
$str = json_encode($data);
$ch = curl_init('http://localhost:8083/api/osinstall/v1/report/deviceMacInfo');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $str);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Content-Length: ' . strlen($str))
);

$result = curl_exec($ch);
echo $result;
```

## 返回参数

字段 | 说明
--- | ---
Status | success/failure
Content.Result | true:成功 false:失败
Message | 提示

## 返回参数示例

```json
{
  "Content": {
    "Result": "true"
  },
  "Message": "操作成功",
  "Status": "success"
}
```
