
# 时间格式转格式
## 使用原生js调用转格式
```
<!-- TODO  -->、
/**
time: 传入的时间戳
dateString：日期的格式（1970-01-19 ）
timeString：时间的格式（13:04:13）
*/
function timeFormat(time, dateString, timeString) {
    if (!time) {
      return "";
    }
    var d = new Date(time);
    var year = d.getFullYear(); //年
    var month = d.getMonth() + 1; //月
    var day = d.getDate(); //日
    var hh = d.getHours(); //时
    var mm = d.getMinutes(); //分
    var ss = d.getSeconds(); //秒
    var clock = year + dateString;
    if (month < 10) clock += "0";
    clock += month + dateString;
    if (day < 10) clock += "0";
    clock += day + " ";
    if (hh < 10) clock += "0";
    clock += hh + timeString;
    if (mm < 10) clock += "0";
    clock += mm + timeString;
    if (ss < 10) clock += "0";
    clock += ss;
    return clock;
  }
  console.log(timeFormat(1573453998,'-',':')) // 1970-01-19 13:04:13
```
## 使用vue转码（filter）
```
<template>
	<div>{{time|timeFormat}}</div>
</template>
<script>
	export default {
		data() {
			return {
				time: 1573453998
			}
		},
		filters: {
			timeFormat(time) {
				if (!time) {
					return "";
				}
				var d = new Date(time);
				var year = d.getFullYear(); //年
				var month = d.getMonth() + 1; //月
				var day = d.getDate(); //日
				var hh = d.getHours(); //时
				var mm = d.getMinutes(); //分
				var ss = d.getSeconds(); //秒
				var clock = year + "-";
				if (month < 10) clock += "0";
				clock += month + "-";
				if (day < 10) clock += "0";
				clock += day + " ";
				if (hh < 10) clock += "0";
				clock += hh + ":";
				if (mm < 10) clock += "0";
				clock += mm + ":";
				if (ss < 10) clock += "0";
				clock += ss;
				return clock;
			}
		}
	}
</script>
```