---
title: 【JavaScript】日期处理集锦
date: 2019-06-15
categories:  JavaScript
tags:
    - 日期
---
针对日期格式的处理，此文整理了一些常用的方法。

<!--more-->

#### 1、将日期对象/日期字会串格式化为指定日期字符串

（1）入参：Date对象
（2）出参：string，格式为yyyy-MM-dd hh:mm:ss
  
    function formatFullDate(sDate,fmt) {
        var sDate = new Date(sDate),
            fmt = fmt||'yyyy-MM-dd hh:mm:ss';
        var o = {
            "M+" : sDate.getMonth()+1,                 //月份
            "d+" : sDate.getDate(),                    //日
            "h+" : sDate.getHours(),                   //小时
            "m+" : sDate.getMinutes(),                 //分
            "s+" : sDate.getSeconds(),                 //秒
            "q+" : Math.floor((sDate.getMonth()+3)/3), //季度
            "S"  : sDate.getMilliseconds()             //毫秒
        };
        if(/(y+)/.test(fmt)) {
            fmt=fmt.replace(RegExp.$1, (sDate.getFullYear()+"").substr(4 - RegExp.$1.length));
        }
        for(var k in o) {
            if(new RegExp("("+ k +")").test(fmt)){
                fmt = fmt.replace(RegExp.$1, (RegExp.$1.length==1) ? (o[k]) : (("00"+ o[k]).substr((""+ o[k]).length)));
            }
        }
        return fmt;
    }


#### 2、将日期对象/日期字会串格式化为指定日期字符串

（1）入参：{object|string}， vArg 可为日期对象或日期字符串，日期对象格式new Date(yyyy, mm,dd)，日期字符串格式yyyy-mm|n-dd|d
（2）出参：string yyyy-mm-dd

	function formatStrDate(vArg) {
		switch (typeof vArg) {
		case "string":
			vArg = vArg.split(/-|\//g);
			return vArg[0] + "-" + this.formatNum(vArg[1]) + "-"
					+ this.formatNum(vArg[2]);
			break;
		case "object":
			return vArg.getFullYear() + "-"
					+ this.formatNum(vArg.getMonth() + 1) + "-"
					+ this.formatNum(vArg.getDate());
			break;
		}
	}


#### 3、格式化数字，不足两位前面补0

（1）入参：number，要格式化的数字
（2）出参：string

	function formatNum(num) {
		return num.toString().replace(/^(\d)$/, "0$1")
	}


#### 4、获取指定日期（yyyy-mm-dd）的前1~3天/后1~3天数据

（1）入参： sDate为日期字符串（yyyy-mm-dd）；dateName为日期名字。
（2）出参：object

	function getThreeDays(sDate, dateName) {
		var oTmp = {}, aDate = sDate.split(/-|\//g), sDate, i;
		for (i = 0; i < 7; i++) {
			sDate = this.formatStrDate(new Date(aDate[0], aDate[1] - 1, aDate[2] - 0 + (i - 3)));
			oTmp[sDate] = dateName
					+ (i != 3 ? (i < 3 ? "\u524d" : "\u540e")
							+ Math.abs(i - 3) + "\u5929" : "");
			i > 2
					&& (_dateMap[sDate] = dateName
							+ (i != 3 ? (i < 3 ? "\u524d" : "\u540e")
									+ Math.abs(i - 3) + "\u5929" : ""))
		}
		return oTmp
	}


#### 5、获取星期信息

（1）入参：date位Date对象；type为“周”，返回周几，默认是返回星期几的。
（2）出参：string类型的星期几

	function getWeek(date,type) {
		var index = date.getDay();
		if(type == "周"){
			var weeks = "周日 周一 周二 周三 周四 周五 周六".split(" ");
		}else{
			var weeks = "星期日 星期一 星期二 星期三 星期四 星期五 星期六".split(" ");
		}
		return weeks[index];
	}


#### 6、获取开始日期后N天日期、星期信息（不包含开始）

（1）入参：startDate为开始日期字符串（yyyy-mm-dd），days为天数，format为出参日期格式。
（2）出参：Array

	function getDateInfos(startDate, days, format) {
		format = format || "yyyy-mm-dd";
		var dateInfos = [];
		
		var dateNums = startDate.split(/-|\//g);
		for(var i = 0; i<= days; i++){
			var date = new Date(dateNums[0], dateNums[1] - 1, dateNums[2] -0 + i);
			var dateStr = this.formatStrDate(date);
			
			var dateInfo = {
				date: dateStr,
				week: this.getWeek(date)
			};
			dateInfos.push(dateInfo)
		}
		return dateInfos;
	}
	

#### 7、获取两个日期间的天数

（1）入参：两个string类型的日期
（2）出参：整型的天数

	function daysBetween(date1, date2){
		var d1 = new Date(date1.replace("-", "/").replace("-", "/")).getTime();
		var d2 = new Date(date2.replace("-", "/").replace("-", "/")).getTime();
		return parseInt((d1 - d2)/(1000*60*60*24)); 
	}


#### 8、解决 ie，火狐浏览器不兼容new Date

(1)入参：string类型的日期
(2)出参：Date对象的日期

	function getDateForStringDate(strDate){
	 	//切割年月日与时分秒称为数组
	 	var s = strDate.split(" "); 
	 	var s1 = s[0].split("-"); 
	 	var s2 = s[1].split(":");
	 	if(s2.length == 2){
	 		s2.push("00");
	 	}
	 	return new Date(s1[0],s1[1]-1,s1[2],s2[0],s2[1],s2[2]);
	}

#### 9、计算日期后若干天的日期

（1）入参：startDate为Date对象，addDays为整型
（2）出参：Date对象的日期

	function addDate(startDate, addDays){
	 	startDate = startDate.valueOf();
	 	startDate = startDate + Number(addDays) * 24 * 60 * 60 * 1000;
	 	return new Date(startDate);
	}


#### 10、计算日期前若干天的日期
（1）入参：startDate为Date对象，delDays为整型
（2）出参：Date对象的日期

    function delDate(startDate, delDays){
        startDate = startDate.valueOf();
	 	startDate = startDate - Number(delDays) * 24 * 60 * 60 * 1000;
	 	return new Date(startDate);
    }


#### 11、获取几号

    function getDay(days){
		return new Date(days).getDay();
	}

	