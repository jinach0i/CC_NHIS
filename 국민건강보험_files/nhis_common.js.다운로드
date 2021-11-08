	/* jQuery Custom Plugin Functions */

	/**
	 * Checkbox 체크 여부를 리턴
	 */
	$.fn.isChecked = function() {
		var result = false;
		
		this.each(function() {
			if(this.checked) {
				result = true;
				return false;
			}
		});
		
		return result;
	};
	
	// 상태 관리를 위한 global 변수
	var G_COMMON = {};
	
	/**
	 * Companion.JS와 연동하여 디버깅 로그를 출력, Companion.JS 적용을 위해 파일 인코딩을 반드시 UTF-8로 설정
	 * 
	 * @param obj 출력하고자 하는 Object
	 * @return void
	 */
	function gfn_debug(obj) {
		if(window.console) {
			console.debug(obj);
		}
	}
	
	/**
	 * event를 발생시킨 Event Source를 리턴
	 * 
	 * @param evt event
	 */
	function gfn_getEventSource(evt) {
		if(evt.target) return evt.target;
		else return evt.srcElement;
	};
	
	/**
	 * 클릭 이벤트 발생 위치를 리턴
	 * @param evt event
	 */
	function gfn_getClickPosition(evt) {
		if(!evt) {
			return {left:0, top:0};
		}
		
		var x, y;
		var obj = gfn_getEventSource(evt);
		
		if(evt.pageX) {
			alert("other: " + evt.pageX);
			x = evt.pageX - obj.offsetLeft;
			y = evt.pageY - obj.offsetTop;
		} else if(evt.clientX) {
			alert("ie: " + evt.clientX);
			x = evt.clientX + document.body.scrollLeft - document.body.clientLeft - obj.offsetLeft;
			y = evt.clientY + document.body.scrollTop - document.body.clientTop - obj.offsetTop;
		} else {
			alert("none");
		}
		
		if(document.body.parentElement && document.body.parentElement.clientLeft) {
			var b = document.body.parentElement;
			x += b.scrollLeft - b.clientLeft;
			y += b.scrollTop - b.clientTop;
		}
		
		// alert(x + "," + y);
		
		return {left:x, top:y};
	}
	
	// AJAX Callback 함수를 위한 변수
	var ajaxCallback;
	
	/**
	 * AJAX Submit
	 * 
	 * @param targetUrl Target URL
	 * @param params Parameters
	 * @param callback Callback function
	 * @param disable disable flag
	 * @return void
	 */
	function gfn_ajaxSubmit(targetUrl, params, callback, disable) {
		/*
		if(showImage!=false) {
			var position = gfn_getEventPosition(G_COMMON.lastEvent);
			var style = "position:absolute;left:" + position.left + "px;top:" + position.top + "px;";
			
			$("#ajaxLoaderImageDiv").remove();
			$("body").append("<div id='ajaxLoaderImageDiv' style='" + style + "'><img id='ajaxLoaderImage' src='/static/images/ajax-loader.gif' /></div>");
		}
		*/
		
		if(disable!=false) {
			G_COMMON.ajaxSourceObject = gfn_getEventSource(G_COMMON.lastEvent);
			$(G_COMMON.ajaxSourceObject).attr("disabled", true);
		}
		
		params["AJAX_PARAM"] = "ajax";
		
		ajaxCallback = callback;
		
		$.ajax({
			url:targetUrl,
			type:'POST',
			data:params,
			dataType:'xml',
			timeout:0,
			error:gfn_ajaxSubmitErrorHandler,
			success:gfn_ajaxSubmitCallback
		});
	}

	/**
	 * AJAX Callback function
	 * 
	 * @param xml 서버에서 수신한 XML 데이터
	 * @return void
	 */
	function gfn_ajaxSubmitCallback(xml) {
		// $("#ajaxLoaderImageDiv").remove();
		$(G_COMMON.ajaxSourceObject).attr("disabled", false);
		
		var sessionCheck = "";

		/*
		$(xml).find("item").each(function() {
			sessionCheck = jQeury("sessionCheck", $(this)).text();
		});
		*/
		
		if(sessionCheck=="false") {
			alert("세션이 만료되어 로그인 페이지로 이동합니다.");

			if(opener) {
				opener.top.location.href = "/";
				self.close();
			} else {
				top.location.href = "/";
			}
		} else {
			ajaxCallback(xml);
		}
	}

	/**
	 * AJAX Submit
	 * 
	 * @param targetUrl Target URL
	 * @param params Parameters
	 * @param callback Callback function
	 * @param disable disable flag
	 * @return void
	 */
	function gfn_ajaxSubmitJson(targetUrl, params, callback, disable) {
		/*
		if(showImage!=false) {
			var position = gfn_getEventPosition(G_COMMON.lastEvent);
			var style = "position:absolute;left:" + position.left + "px;top:" + position.top + "px;";
			
			$("#ajaxLoaderImageDiv").remove();
			$("body").append("<div id='ajaxLoaderImageDiv' style='" + style + "'><img id='ajaxLoaderImage' src='/static/images/ajax-loader.gif' /></div>");
		}
		*/
		
		if(disable!=false) {
			G_COMMON.ajaxSourceObject = gfn_getEventSource(G_COMMON.lastEvent);
			$(G_COMMON.ajaxSourceObject).attr("disabled", true);
		}
		params["AJAX_PARAM"] = "ajax";
		
		ajaxCallback = callback;
		
		$.ajax({
			url:targetUrl,
			type:'POST',
			data:params,
			dataType:'json',
			timeout:0,
			error:gfn_ajaxSubmitErrorHandler,
			success:gfn_ajaxSubmitJsonCallback
		});
	}
	
	/**
	 * AJAX Callback function
	 * 
	 * @param xml 서버에서 수신한 XML 데이터
	 * @return void
	 */
	function gfn_ajaxSubmitJsonCallback(json) {
		// $("#ajaxLoaderImageDiv").remove();
		$(G_COMMON.ajaxSourceObject).attr("disabled", false);
		
		var sessionCheck = "";

		/*
		$(xml).find("item").each(function() {
			sessionCheck = jQeury("sessionCheck", $(this)).text();
		});
		*/
		
		if(sessionCheck=="false") {
			alert("세션이 만료되어 로그인 페이지로 이동합니다.");

			if(opener) {
				opener.top.location.href = "/";
				self.close();
			} else {
				top.location.href = "/";
			}
		} else {
			ajaxCallback(json);
		}
	}
	
	
	/**
	 * AJAX Error Handler
	 * 
	 * @param XMLHttpRequest XMLHttpRequest
	 * @param textStatus Status
	 * @param errorThrown Error
	 * @return void
	 */
	function gfn_ajaxSubmitErrorHandler(XMLHttpRequest, textStatus, errorThrown) {
		// $("#ajaxLoaderImageDiv").remove();
		$(G_COMMON.ajaxSourceObject).attr("disabled", false);

		if(textStatus=="parsererror") {
			alert("서버에서 에러가 발생하였습니다. 관리자에게 문의하십시오.");
		} else if(textStatus=="error") {
			alert("서버가 응답하지 않습니다. 관리자에게 문의하십시오.");
		} else {
			alert("[" + textStatus + "]");
		}
	}
	
	/**
	 * AJAX 호출 결과 XML을 Select Box Option에 추가
	 * 
	 * @param objId Select Box ID
	 * @param xml XML Data
	 * @param nameAndValue Name, Value로 사용할 Element Name
	 * @param selectedValue 선택된 값
	 */
	function gfn_setSelectBox(objId, xml, nameAndValue, selectedValue) {
		var obj = $("#" + objId);
		
		var nameAndValueArr = nameAndValue.split(",");
		var nameElementName = nameAndValueArr[0];
		var valueElementName = nameAndValueArr[1];
		
		// option 삭제
		obj.empty();

		// option 추가
		$(xml).find("item").each(function() {
			var item = $(this);

       		//cfDebug($("value", item).text() + "/" + $("text", item).text());
			
			// 조회조건 유지
			var selected = "";
			
			if(selectedValue && selectedValue==$(valueElementName, item).text()) {
				selected = "selected";
			}
			
       		var option = "<option value='" + $(valueElementName, item).text() + "' " + selected + ">"
       		           + $(nameElementName, item).text()
                       + "</option>";
       		
			obj.append(option);
		});
	}

	/**
	 * 달력 팝업 오픈
	 * 
	 * @param objectId
	 * @param evt
	 * @param startYear
	 * @param endYear
	 * @param callback
	 * @param fixed
	 * @return void
	 */
	function gfn_openCalendar(objectId, evt, startYear, endYear, callback, fixed) {
		var extendParam = "";

		if(startYear!=null && startYear!="" && endYear!=null && endYear!="") {
			extendParam += "&startYear=" + startYear + "&endYear=" + endYear;
		}

		if(callback!=null && callback!="") {
			extendParam += "&callback=" + callback;
		}

		var orgVal = $("#" + objectId).val();
		if(orgVal != ''){
			orgVal = orgVal.replaceAll(".", "");
			var year = orgVal.substring(0, 4);
			var month = parseInt(orgVal.substring(4, 6), 10) - 1; // 0으로 시작하면 반드시 10진수 처리
			
			extendParam += "&year=" + year;
			extendParam += "&month=" + month;
		}
		
		var url = "/common/openCalendar.do?objectId=" + objectId + extendParam;
		var winName = "Calendar";
		var winProps = "toolbar=0,location=0,directories=0,status=0,menubar=0,scrollbars=no,resizable=yes,"
		             + "width=230px,height=225px,left=" + evt.screenX + ",top=" + evt.screenY;
		var win = window.open(url, winName, winProps);

		win.focus();
	}
	
	/**
	 * 파일 다운로드
	 * 
	 * @param fileName 저장되는 파일명
	 * @param filePath 서버에 저장된 파일 경로
	 * @return void
	 */
	function gfn_downloadFile(fileName, filePath) {
		$("#fileDownload").remove();
		$("body").append("<iframe id='fileDownload' width='0' height='0' />");
		$("#fileDownload")[0].src = encodeURI("/common/downloadFile.do?fileName=" + fileName + "&filePath=" + filePath);
	}

	/**
	 * 파일 다운로드 (파일 ID 를 이용한 다운로드 처리)
	 * 
	 * @param fileName 저장되는 파일명
	 * @param filePath 서버에 저장된 파일 경로
	 * @return void
	 */
	function gfn_downloadFileByID(id) {
		$("#fileDownload").remove();
		$("body").append("<iframe id='fileDownload' width='0' height='0' />");
		$("#fileDownload")[0].src = encodeURI("/common/nhisDownloadFile.do?id=" + id);
	}
	
	/**
	 * 테이블 hover시 Lhover 클래스 부여
	 */
	function gfn_applyStyleListTable () {
		$(".LblockListTable table tr").each(function() {
			var tr = $(this);
			
			tr.mouseover(function() {
				tr.addClass("Lhover");
			});
			tr.mouseout(function() {
				tr.removeClass("Lhover");
			});
		});
	}
	
	/**
	 * 날짜를 비교하여 차이값을 정수값으로 리턴,
	 * 0이면 동일한 날짜,
	 * 양수이면 fromDateStr가 toDateStr보다 큼
	 * 음수이면 fromDateStr가 toDateStr보다 작음
	 *
	 * @param fromDateStr 시작일자
	 * @param toDateStr 종료일자
	 * @return 차이값
	 */
	function gfn_compareDate(fromDateStr, toDateStr) {
		var fromDateArr = fromDateStr.split("-");
		var toDateArr = toDateStr.split("-");
		var fromDate = new Date(parseInt(fromDateArr[0]), parseInt(fromDateArr[1])-1, parseInt(fromDateArr[2]));
		var toDate = new Date(parseInt(toDateArr[0]), parseInt(toDateArr[1])-1, parseInt(toDateArr[2]));
		var gap = Math.floor( (fromDate.getTime() - toDate.getTime()) / (60*60*24*1000) );

		return gap;
	}
	 
	/**
	 * Cookie 설정
	 */
	function gfn_setCookie(name, value, expires, path, domain, secure) {
		var today = new Date();
		today.setTime(today.getTime());
		
		if(expires) {
			expires = expires * 1000 * 60 * 60 * 24; // x number of days
		}
		
		var expiresDate = new Date(today.getTime() + expires);
		
		document.cookie = name + "=" + escape(value)
		                + ( expires ? ";expires="+expiresDate.toGMTString() : "" )
		                + ( path ? ";path="+path : "" )
		                + ( domain ? ";domain="+domain : "" )
		                + ( secure ? ";secure" : "" );
	}
	
	/**
	 * Cookie 가져오기
	 */
	function gfn_getCookie(name) {
		var bInx = document.cookie.indexOf(name);
		var eInx = 0;
		
		if(bInx==-1) return "";
		
		bInx = bInx + name.length + 1;
		eInx = document.cookie.indexOf(";", bInx);
		
		if(eInx==-1) eInx = document.cookie.length;
		
		var result = document.cookie.substring(bInx, eInx);
		
		return unescape(result);
	}
	 
	/**
	 * URL로부터 File Name을 리턴
	 */
	function gfn_getFileNameFromUrl(url) {
		var fileName = url.substring(url.lastIndexOf("/") + 1);
		return fileName;
	}
	
	
	/**
	 * 월 선택에 따른 일자 SelectBox 값 변경.
	 */
	function gfn_setDayRange(selMonth, selDay){
		
		var arr = null;
		var arr1 = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31'];
		var arr2 = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', '25', '26', '27', '28', '29', '30'];
		var arr3 = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', '25', '26', '27', '28'];
		
		
		var this_ = $("#" + selMonth);
		var obj = $("#" + selDay);
		
		if( obj != null){
			
			obj.empty();
			if(this_.val() == '02'){
				arr = arr3;
			}else if(this_.val() == '01' ||
					this_.val() == '03' ||
					this_.val() == '05' ||
					this_.val() == '07' ||
					this_.val() == '08' ||
					this_.val() == '10' || 
					this_.val() == '12'){
				arr = arr1;    				
			} else {
				arr = arr2;
			}
			
			for(i = 0; i < arr.length; ++i){
				obj.append("<option value=\"" + arr[i] + "\">" + arr[i] +"</option>");
			}
		} 
	}
	
	/**
	 * 페이지 로드 시 초기화 함수
	 */
	$(document).ready(function() {
		$(document).bind("click", function(event) {
			G_COMMON.clickEvent = event;
			G_COMMON.lastEvent = event;
		});
		$(document).bind("keydown", function(event) {
			G_COMMON.keydownEvent = event;
			G_COMMON.lastEvent = event;
		});
		
		// gfn_applyStyleListTable();
	});

	
	function displaySub(id){
		for(i=1; i<20; i++){
			var subID = "submenu" + i;
			if(i == id){
				document.getElementById(subID).className = 'yes';
			}else{
				document.getElementById(subID).className = 'no';
			}
		}
	}
	
	
	// 지역본부 클릭시 해당하는 지사를 보여주거나 숨긴다
	function showHide(strID) {
		var iCount = 6; 
		
		for(iTbl=1; iTbl <= iCount; iTbl++) {
			document.getElementById('LinkTbl' + iTbl).style.display = (iTbl == strID) ? 'block' :  'none';
		} 
	}

	function showHide2() {
		document.getElementById('jisa').style.display = "";
	}
	
	// 지역본부 갯수
	function jisaShow() {
		var iCount = 6; 
	
		if (!document.getElementsByTagName || !document.createTextNode) return;

		for(iTbl=1; iTbl <= iCount; iTbl++) {
    		// 작업대상 테이블
    		var objTbl = document.getElementById('LinkTbl' + iTbl);
    		objTbl.style.cursor = 'hand';
    		
    		var rows = objTbl.getElementsByTagName('tbody')[0].getElementsByTagName('tr');
    
    		for (i = 0; i < rows.length; i++) {
    			
    			var cols = rows[i].getElementsByTagName('td');
    			
    			for(j = 0; j < cols.length; j++) {
	        		//rows[i].onclick = function() {
	        		cols[j].onclick = function() {
		        			if ( this.innerText.length > 2 ) {
		        				//alert(this.innerText.length);
		        				var strURL = "/wbd/fc/retrieveLinkEmployeeList.xx?partCd=" + this.innerText;
		            			//window.open(strURL, "srchWin");
		            			 location.replace(strURL);
		            		} // if
	        		} // function
	        	}	// j
    		} // i
    	} // iTbl
	}
	
	
	// 이메일 형식 체크
	function checkEmail(checkString) {
		var atnum=0;
		var apoint=0;
		var a_endpoint=0;
		var d_endpoint=0;
		var dpoint=0;
		var str_length;
		var ch;

		str_length=checkString.length-1;
		apoint=checkString.indexOf("@");
		a_endpoint=checkString.lastIndexOf("@");
		
		if (apoint!=-1) {
			if ((apoint==0) || (a_endpoint==str_length))
				return false;
		} else {
			return false;
		}		

		dpoint=checkString.indexOf(".");
		d_endpoint=checkString.lastIndexOf(".");
		
		if (dpoint!=-1) {
				if ((dpoint==0) || (d_endpoint==str_length) )
					return false;
		} else {
			return false;
		}
		
		for (var i=0;i <= str_length;i++) {
			ch=checkString.charAt(i);
			if ((ch >= "A" && ch <= "Z") || (ch >= "a" && ch <= "z") || (ch=="@") || (ch==".") || (ch=="-") || (ch=="_") || (ch >= "0" && ch <= "9")) {
				if (ch=="@") {
					atnum=atnum +1;
					if (atnum > 1) {
						return false;
						break;
					}
				}
				if (ch==".") {
					if ((checkString.charAt(i-1)=="@") || (checkString.charAt(i+1)==".")) {
						return false;
						break;
					}
				}
			} else {
				return false;
				break;
			}
		}
		return true;
	}
		
	