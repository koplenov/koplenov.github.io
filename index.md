<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<!-- Mirrored from www.ip-ping.ru/netcalc/ by HTTrack Website Copier/3.x [XR&CO'2017], Tue, 29 Oct 2019 05:47:39 GMT -->
<!-- Added by HTTrack --><meta http-equiv="content-type" content="text/html;charset=windows-1251" /><!-- /Added by HTTrack -->
<head><title>������� �����������, IP ����������� </title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<link rel="stylesheet" href="../style.css" type="text/css">
<!--[if lt IE 7]>
<script type="text/javascript" src="../../cdnjs.cloudflare.com/ajax/libs/prototype/1.7.3/prototype.min.js"></script>
<script type="text/javascript">
  Event.observe(window, 'load', function(){
        $$('table.menu td.menu_item').each(function(td){
              td.onmouseover  = function(){ this.addClassName('active_menu'); }
              td.onmouseout  = function(){  this.removeClassName('active_menu');  }
        });
  });
	</script>
	
<![endif]-->
</head>
<body>
<table class="container">
<tr>
<td class="left_col">&#160;</td>
<td class="for_content">
<table class="container2">
<tr>
<td class="center" colspan="2">
<table class="content">
<tr>
<td class="l">
<td class="c">
	<script>
    var md = new MobileDetect(window.navigator.userAgent);
jQuery( document ).ready(function() {
        if (md.phone()) {
            jQuery( "#post_top_d" ).remove();
        }
    if (md.tablet()) {
        jQuery( "#post_top_m" ).remove();
        }
    if (!md.mobile()) {
        jQuery( "#post_top_m" ).remove();
        }
});
</script>
<script language="javascript" type="text/javascript">
nGlobal=0;
function mySetInnerText(element, txt) {
	try {
		element.innerText = txt;
	} catch (e) { }
	try {
		element.textContent = txt;
	} catch (e) { }
}
function ClearBroadcast(f) {
  f.Broadcast.value = "";
  f.Network.value = "";
  f.HostAmnt.value = "";
}
function Len2MaskCalc(nMask) {
	if (nMask < 1) {
		return 0;
	}
	nCalc = 0;
	for (nX = 7;nX > -1 ; nX--) {
		nCalc=nCalc + raiseP(2 , nX);
		nMask = nMask -1;
		nGlobal=nMask;
		if (nMask <1) {
			return nCalc;
		}
	}
	return nCalc;
}
function raiseP(x,y) {
  total=1;
  for (j=0; j < y; j++) {
  	total*=x;
  }
  return total;
}
function CalcLen2Mask(f) {
  try {
  if ((f.MaskLen.value < 0)|| (f.MaskLen.value>32)) {
    mySetInnerText($('maskCalcMsg'), '(����� � �������� 0 - 32)');
    f.IP1.value = '';
    f.IP2.value = '';
    f.IP3.value = '';
    f.IP4.value = '';
    return 0;
  }
  nMaskLen = f.MaskLen.value;
  f.IP1.value=Len2MaskCalc(nMaskLen);
  f.IP2.value=Len2MaskCalc(nGlobal);
  f.IP3.value=Len2MaskCalc(nGlobal);
  f.IP4.value=Len2MaskCalc(nGlobal);
  } catch (e) {
    mySetInnerText($('maskCalcMsg'), '(��������� ������� ������)');
    f.IP1.value = '';
    f.IP2.value = '';
    f.IP3.value = '';
    f.IP4.value = '';
    return 0;
  }
    mySetInnerText($('maskCalcMsg'), '');
}
function CalcMask2Len(f) {
	try {
	var m = new Array(1,2,3,4);
	m[0] = f.IP1.value; m[1] = f.IP2.value;
	m[2] = f.IP3.value; m[3] = f.IP4.value;
	ipcheck=TestSN(m[0],m[1],m[2],m[3]);
	if (ipcheck > 0) {
	    	mySetInnerText($('maskLenMsg'), '(������������ ����� �������)');
		f.MaskLen.value = '';
		return 0;
	}
	mask = 0;
	for (loop=0; loop<4; loop++) {
		div = 256;
		while (div > 1) {
			div = div/2;
			test = m[loop]-div;
			if ( test >-1) {
				mask=mask+1;
				m[loop]=test;
			} else {
				break;
			}
		}
	}
	f.MaskLen.value = mask;
	} catch (e) {
	    	mySetInnerText($('maskLenMsg'), '(��������� ������� ���������)');
		f.MaskLen.value = '';
		return 0;
	}
    	mySetInnerText($('maskLenMsg'), '');
}
function CalcBroadcast(f) {
  ClearBroadcast(f);
  try {
  var ipcheck=TestIP(f.IP1.value,f.IP2.value,f.IP3.value,f.IP4.value);
  if (ipcheck > 0) {
	mySetInnerText($('networkCalcMsg'), '(������������ IP �����)');
	ClearBroadcast(f);
  	return 0;
  }
  ipcheck=TestSN(f.SN1.value,f.SN2.value,f.SN3.value,f.SN4.value);
  if (ipcheck > 0) {
	mySetInnerText($('networkCalcMsg'), '(������������ ����� �������)');
	ClearBroadcast(f);
  	return 0;
  }
  var nOctA1=f.IP1.value & f.SN1.value;
  var nOctA2=f.IP2.value & f.SN2.value;
  var nOctA3=f.IP3.value & f.SN3.value;
  var nOctA4=f.IP4.value & f.SN4.value;
  var nOctB1=f.IP1.value | (f.SN1.value ^ 255);
  var nOctB2=f.IP2.value | (f.SN2.value ^ 255);
  var nOctB3=f.IP3.value | (f.SN3.value ^ 255);
  var nOctB4=f.IP4.value | (f.SN4.value ^ 255);
  f.Broadcast.value = nOctB1+"."+nOctB2+"."+nOctB3+"."+nOctB4;
  f.Network.value = nOctA1+"."+nOctA2+"."+nOctA3+"."+nOctA4;
  var nHosts = ((~f.SN1.value & 255) << 24) + ((~f.SN2.value & 255) << 16) + ((~f.SN3.value & 255) << 8) + (~f.SN4.value & 255) + 1;
  f.HostAmnt.value = nHosts;
  } catch (e) { 	mySetInnerText($('networkCalcMsg'), '(��������� ������� ������)'); ClearBroadcast(f); return 0; }
  mySetInnerText($('networkCalcMsg'), '');
}
function CalcOnNetwork(f) {
	try {
	var ipcheck=TestIP(f.IP1.value,f.IP2.value,f.IP3.value,f.IP4.value);
	if (ipcheck > 0) {
		f.Answer.value = "(������������ IP �����)";
		return 0;
	}
	ipcheck=TestSN(f.SN1.value,f.SN2.value,f.SN3.value,f.SN4.value);
	if (ipcheck > 0) {
		f.Answer.value = "(������������ ����� �������)";
		return 0;
	}
	ipcheck=TestIP(f.SP1.value,f.SP2.value,f.SP3.value,f.SP4.value);
	if (ipcheck > 0) {
		f.Answer.value = "(������������ IP ����� 2)";
		return 0;
	}
	var nOctA1=f.IP1.value & f.SN1.value
	var nOctA2=f.IP2.value & f.SN2.value
	var nOctA3=f.IP3.value & f.SN3.value
	var nOctA4=f.IP4.value & f.SN4.value
	var nOctB1=f.SP1.value & f.SN1.value
	var nOctB2=f.SP2.value & f.SN2.value
	var nOctB3=f.SP3.value & f.SN3.value
	var nOctB4=f.SP4.value & f.SN4.value
	if ((nOctA1==nOctB1) && (nOctA2==nOctB2) && (nOctA3==nOctB3) && (nOctA4==nOctB4)) {
		f.Answer.value ="� ����� ����";
	} else {
		f.Answer.value ="� ������ �����";
	}
	return 0;
	} catch (e) {
		f.Answer.value = '(��������� ������� ���������)';
		return 0;
	}
	f.Answer.value = '';
}
function CalcNetworks(f) {
	var ipcheck=TestIP(f.IP1.value,f.IP2.value,f.IP3.value,f.IP4.value);
	if (ipcheck > 0) {
		alert("������������ IP �����!");
		return 0;
	}
	alert("ai address are ok");
}
function TestIP(IP1, IP2, IP3, IP4) {
	if ((IP1 > 255) || (IP1 < 1) || (IP1 == '')) { return 1; }
	if ((IP2 > 255) || (IP2 < 0) || (IP2 == '')) { return 2; }
	if ((IP3 > 255) || (IP3 < 0) || (IP3 == '')) { return 3; }
	if ((IP4 > 255) || (IP4 < 0) || (IP4 == '')) { return 4; }
	return 0;
}
function TestSN(IP1, IP2, IP3, IP4) {
	if ((IP1 > 255) || (IP1 < 0) || (IP1 == '')) { return 1; }
	if ((IP2 > 255) || (IP2 < 0) || (IP2 == '')) { return 2; }
	if ((IP3 > 255) || (IP3 < 0) || (IP3 == '')) { return 3; }
	if ((IP4 > 255) || (IP4 < 0) || (IP4 == '')) { return 4; }
	var IPX =5;
	if (IP1 < 255) {
		if((IP2 > 0) || (IP3 > 0) || (IP4 > 0)) {
			return 5;
		}
		IPX = IP1;
	} else {
		if (IP2 < 255) {
			if((IP3 > 0) || (IP4 > 0)) {
				return 6;
			}
			IPX = IP2;
		} else {
			if (IP3 < 255) {
				if ((IP4 > 0)) {
					return 7;
				}
				IPX = IP3;
			} else {
				IPX = IP4;
			}
		}
	}
	switch (IPX) {
		case "255": case "128": case "192": case "224": case "240": case "248": case "252": case "254": case "0": {
			return 0;
		}
		default: {
			return 8;
		}
	} return 0;
}
</script>
<p><div class='form'>
<form name="networkCalc" style='margin: 0px;'>
<table width="550" class="ResTableAjax" cellspacing="5" cellpadding="0" border="0" style='font-size: 12px;'>
<tr>
<td width="250" align="left">Введите ваш IP адрес:</td>
<td pwoie="1" pta5n="5"><input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="IP1" type="text" />&bull;<input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="IP2" type="text" />&bull;<input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="IP3" type="text" />&bull;<input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="IP4" type="text" /></td>
</tr>
<tr>
<td align="left">Введите маску вашей сети:</td>
<td pwoie="1" pta5n="5"><input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="SN1" value="255" type="text" />&bull;<input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="SN2" value="255" type="text" />&bull;<input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="SN3" value="255" type="text" />&bull;<input maxlength="3" size="3" onkeyup="CalcBroadcast(this.form)" onchange="CalcBroadcast(this.form)" name="SN4" value="0" type="text" /></td>
</tr>
<tr>
<th align="left" colspan="2">Результаты  <span id="networkCalcMsg" style="font-weight: bold; color: red">&nbsp;</span></th>
</tr>
<tr>
<td align="left">Количество хостов:</td>
<td><input name="HostAmnt" type="text" /></td>
</tr>
<tr>
<td align="left">Широковещательный адрес:</td>
<td><input name="Broadcast" type="text" /></td>
</tr>
<tr>
<td align="left">Сетевой адрес:</td>
<td><input name="Network" type="text" /></td>
</tr>
</table>
</form>
</div>
</p>
</td>
</table>
</body>

<!-- Mirrored from www.ip-ping.ru/netcalc/ by HTTrack Website Copier/3.x [XR&CO'2017], Tue, 29 Oct 2019 05:47:59 GMT -->
</html>

</div>
</body>
</html>
