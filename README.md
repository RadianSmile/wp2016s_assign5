# Weather 作業
作業說明：https://goo.gl/lPGaqR

### 補充提示：要怎麼拿到 Yahoo 天氣資料？
1. 打開連結 https://developer.yahoo.com/weather/
2. 直接看到他的第一個 example `Forecast for Nome, AK`
3. YQL Query 那個欄位是指說，如果用 yql 的方式，要怎麼撰寫他的 query
4. 仔細看 yql 欄位裡 `where text="nome, ak"` 這裡就是在指定地區。你可以試著把 `nome, ak` 換成 `Taipei City` ，然後點選 Test。
5. 閱讀 Response 區域裡面的資料，找看看你要的資訊放在哪個節點裡。
6. 複製下方的 endpoint 貼到網址列打開，這就是一個標準的 json 檔案了，裡面放著 `Taipei City` 的天氣資料。
7. 用 jquery 對他 getJSON 就可以在 callback function 裡面拿到資料了。
```javascript
$.getJSON("http://某縣市的 endpoint url ",function(data){
	// 可以比較方便找到你要的資料在這個物件的哪個位置
	console.log (data) ;

	// 例如如果要拿取該縣市的目前溫度。
	var currentTemperature = data.query.results.channel.item.condition.temp  ;
}
```
8. 溫度單位可以選擇直接指定 api 回傳特定溫度單位，或自己在 js 裡面做轉換。如果想要直接指定溫度，可自行研究此[官方文件](https://developer.yahoo.com/weather/documentation.html)

### 補充提示：要怎麼使用 Skycon 圖示？
1. 作業檔案裡面的 js 已經有示範怎麼使用了
2. 要怎麼知道 skycon 有哪些天氣圖示呢？我會這樣做。作業檔案裡面的 js 已經知到這樣可以叫出陰天：
```javascript
skycons.add("today", Skycons.PARTLY_CLOUDY_DAY);
```
那我就用 `PARTLY_CLOUDY_DAY` 到原始碼裡面找看看他在哪裡，就能在原始碼的那個區塊附近看到看到其他更多的天氣關鍵字了。

### 補充提示：從 yahoo 那裡得到的天氣，要怎麼轉換成 skycon 的天氣關鍵字？
1. 首先就要先知道 yahoo 會回傳的天氣關鍵字有哪些，接這透過如 if 或 switch 得方式，將所有常見的 yahoo 的天氣關鍵字轉換成 skycon 的天氣關鍵字，就可以了。
