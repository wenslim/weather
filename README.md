<h1 align="center">Weather</h1>
<p align="center">
基于「[高德开放平台」的`PHP`天气信息组件
</p>

[![Build Status](https://travis-ci.org/wenslim/weather.svg?branch=master)](https://travis-ci.org/wenslim/weather)
![StyleCI build status](https://github.styleci.io/repos/190960988/shield)

#### 安装
```
$ composer require wenslim/weather -vvv
```
#### 配置
在使用本扩展之前，需要「[高德开放平台](https://lbs.amap.com/dev/index)」注册账号，创建应用，并获取应用的 API Key。
#### 基本使用
```
use Wenslim\Weather\Weather;

$key = 'xxxxxx';
$weather = new Weather($key);
```
#### 获取实时天气
```
$response = $weather->getLiveWeather('上海');
```
示例：
```
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "上海",
            "city": "上海市",
            "adcode": "310000",
            "weather": "阴",
            "temperature": "26",
            "winddirection": "西北",
            "windpower": "≤3",
            "humidity": "59",
            "reporttime": "2019-06-08 10:49:45"
        }
    ]
}
```
#### 获取近期天气预报
```
$response = $weather->getForecastsWeather('上海', 'all');
```
示例：
```
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "forecasts": [
    {
        "city": "上海市",
        "adcode": "310000",
        "province": "上海",
        "reporttime": "2019-06-08 10:49:45",
        "casts": [
        {
            "date": "2019-06-08",
            "week": "6",
            "dayweather": "多云",
            "nightweather": "多云",
            "daytemp": "29",
            "nighttemp": "21",
            "daywind": "东南",
            "nightwind": "东南",
            "daypower": "≤3",
            "nightpower": "≤3"
        },
        {
            "date": "2019-06-09",
            "week": "7",
            "dayweather": "多云",
            "nightweather": "多云",
            "daytemp": "30",
            "nighttemp": "22",
            "daywind": "东南",
            "nightwind": "东南",
            "daypower": "≤3",
            "nightpower": "≤3"
        },
        {
            "date": "2019-06-10",
            "week": "1",
            "dayweather": "小雨",
            "nightweather": "多云",
            "daytemp": "30",
            "nighttemp": "21",
            "daywind": "东北",
            "nightwind": "东北",
            "daypower": "4",
            "nightpower": "4"
        },
        {
            "date": "2019-06-11",
            "week": "2",
            "dayweather": "多云",
            "nightweather": "多云",
            "daytemp": "29",
            "nighttemp": "21",
            "daywind": "东",
            "nightwind": "东",
            "daypower": "4",
            "nightpower": "4"
        }]
    }]
}
```
#### 获取 XML 格式返回值
第三个参数为返回值类型，可选 `json` 与 `xml`，默认 `json`：
```
$response = $weather->getLiveWeather('上海', 'xml');
```
示例
```
<response>
    <status>1</status>
    <count>1</count>
    <info>OK</info>
    <infocode>10000</infocode>
    <lives type="list">
        <live>
            <province>上海</province>
            <city>上海市</city>
            <adcode>310000</adcode>
            <weather>晴</weather>
            <temperature>26</temperature>
            <winddirection>西北</winddirection>
            <windpower>≤3</windpower>
            <humidity>69</humidity>
            <reporttime>2019-06-09 11:18:31
            </reporttime>
        </live>
    </lives>
</response>
```
#### 参数说明
```
array|string getLiveWeather(string $city, string $format = 'json')
```
> - $city - 城市名，比如：“上海”；
> - $format - 输出的数据格式，默认为 json 格式，当 output 设置为 “xml” 时，输出的为 XML 格式的数据。
#### 在`laravel`中使用
配置写在`config/services.php`中
```
    .
    .
    .
    'weather' => [
        'key' => env('WEATHER_API_KEY'),
    ],
```
`.env`中配置`WEATHER_API_KEY`：
```
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxxxxx
```
可以用两种方式来获取`Wenslim\Weather\Weather`实例：
##### 方法参数注入
```
use Wenslim\Weather\Weather;

public function show(Weather $weather)
{
    $response = $weather->getLiveWeather('上海');
}
```
##### 服务名访问
```
public function show(Weather $weather)
{
    $response = app('weather')->getLiveWeather('上海');
}
```
#### License
MIT