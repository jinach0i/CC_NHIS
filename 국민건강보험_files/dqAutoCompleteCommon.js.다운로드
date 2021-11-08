
//브라우져 종류 체크 IE/ETC
function dqc_getBrowserType() {
	
	var agent = navigator.userAgent.toLowerCase();
    if ((navigator.appName == "Netscape" && navigator.userAgent.search('Trident') != -1) || (agent.indexOf("msie") != -1)){
    	 return 1;
    }else if (agent.indexOf("chrome") != -1){
    	 return 1;
    }else if (agent.indexOf("firefox") != -1){
    	 return 2;
    }else{
    	return 1;
    }
        
}

//create XMLHTTP 
function dqc_getXMLHTTP(xmlRequest) {
    if (xmlRequest && xmlRequest.readyState != 0)
        xmlRequest.abort();

    try {
        xmlRequest = new ActiveXObject("Msxml2.XMLHTTP");
    }
    catch (e) {
        try {
            xmlRequest = new ActiveXObject("Microsoft.XMLHTTP");
        }
        catch (e) {
            xmlRequest = false;
        }
    }

    if (!xmlRequest && typeof XMLHttpRequest != "undefined")
        xmlRequest = new XMLHttpRequest();

    return xmlRequest;
}

//trim, 공백제거
function dqc_trimSpace(ke) {
    ke = ke.replace(/^ +/g, "");
    ke = ke.replace(/ +$/g, " ");

    ke = ke.replace(/^ +/g, " ");
    ke = ke.replace(/ +$/g, "");

    ke = ke.replace(/ +/g, " ");

    return ke;
}

//문장 하이라이팅
function dqc_highlight(s, d, is_suf, sTag, eTag) {
    var ret = "";

    if (is_suf == 0)
        ret = dqc_makehigh_pre(s, d, sTag, eTag);
    else if (is_suf == -1)
        ret = dqc_makehigh_suf(s, d, sTag, eTag);
    else
        ret = dqc_makehigh_mid(s, d, is_suf, sTag, eTag);

    if (ret == "")
        return s;
    else
        return ret;
}

//앞부분 단어 하이라이팅
function dqc_makehigh_pre(s, t, sTag, eTag) {
    var d = "";
    var s1 = s.replace(/ /g, "");
    var t1 = t.replace(/ /g, "");

    t1 = t1.toLowerCase();
    s1 = s1.toLowerCase();

    if (t1 == s1.substring(0, t1.length)) {
        d = sTag;

        for (var i = 0, j = 0; j < t1.length; i++) {
            if (s.substring(i, i + 1) != " ")
                j++;
            d += s.substring(i, i + 1);
        }

        d += eTag + s.substring(i, s.length)
    }
    return d;
}

//뒷부분 단어 하이라이팅
function dqc_makehigh_suf(s, t, sTag, eTag) {
    var d = "";
    var s1 = s.replace(/ /g, "");
    var t1 = t.replace(/ /g, "");

    t1 = t1.toLowerCase();
    s1 = s1.toLowerCase();

    if (t1 == s1.substring(s1.length - t1.length)) {
        for (var i = 0, j = 0; j < s1.length - t1.length; i++) {
            if (s.substring(i, i + 1) != " ")
                j++;
            d += s.substring(i, i + 1);
        }

        d += sTag;

        for (var k = i, l = 0; l < t1.length; k++) {
            if (s.substring(k, k + 1) != " ")
                l++;
            d += s.substring(k, k + 1);
        }

        d += eTag;
    }

    return d;
}

//중간부분 단어 하이라이팅
function dqc_makehigh_mid(s, t, pos, sTag, eTag) {
    var d = "";
    var s1 = s.replace(/ /g, "");
    var t1 = t.replace(/ /g, "");

    t1 = t1.toLowerCase();
    s1 = s1.toLowerCase();

    d = s.substring(0, pos);
    d += sTag;

    for (var i = pos, j = 0; j < t1.length; i++) {
        if (s.substring(i, i + 1) != " ")
            j++;
        d += s.substring(i, i + 1);
    }

    d += eTag + s.substring(i, s.length);

    return d;
}

//string length
function dqc_strlen(s) {
    var i, l = 0;

    for (i = 0; i < s.length; i++) {
        if (s.charCodeAt(i) > 127)
            l += 2;
        else
            l++;
    }

    return l;
}

//string substring
function dqc_substring(s, start, len) {
    var i, l = 0; d = "";

    for (i = start; i < s.length && l < len; i++) {
        if (s.charCodeAt(i) > 127)
            l += 2;
        else
            l++;

        d += s.substr(i, 1);
    }

    return d;
}