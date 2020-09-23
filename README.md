<div align="center">

## PHP Calendar System


</div>

### Description

This is the beginning of a complete PHP Calendar System that I decided to write. The code that is here will display a calender of the entire year that the user chooses. I found a script somewhat similar to this a while back, and have used it's ideas to build this one. I would credit the author, but I don't remember who it was.

Regardless, I am planning on making a complete calendar system for appointments, important dates, or anything else of that nature.

As it stands now, I haven't commented the source, and hard coded a few things here and there. In the next version which is coming soon, I plan on making the customization much easier. Feedback is encouraged.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[bleh](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/bleh.md)
**Level**          |Intermediate
**User Rating**    |3.8 (15 globes from 4 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__8-1.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/bleh-php-calendar-system__8-774/archive/master.zip)





### Source Code

```
<html>
<head>
<style>
td { font-family: Verdana; font-size: 12px; }
.month { background-color: #2861a6; color: #ffffff; font-weight: bold; }
.day { background-color:#b0c4de; color: #000000; text-align: center; }
</style>
<script>
function changeBG(objRow, sState)
{
	var theCell = document.getElementById(objRow);
	if (sState == "over")
	{ theCell.style.backgroundColor="#1e90ff"; }
	else
	{ theCell.style.backgroundColor="#b0c4de"; }
}
</script>
<title>PHP Calender System</title>
</head>
<?
if (!$curYear){$curYear=date("Y");}
$cellCount=0;
$mainTableCellCount=0;
echo "<table cellpadding=\"2\" cellspacing=\"2\" align=\"center\">\r";
for ($curMonth=1;$curMonth<=12;$curMonth++)
{
	if ($mainTableCellCount == 0) { echo "<tr>\r"; }
	echo "<td align=\"center\" valign=\"top\">\r";
	$curDay=1;
	$thisMonth=$curMonth;
	while($curMonth==$thisMonth)
	{
		$thisMonth=date("m",mktime(23,59,59,$curMonth,$curDay,$curYear));
		$totalDays=date("d",mktime(23,59,59,$curMonth,$curDay-1,$curYear));
		$curDay++;
	}
	$monthTextual=date("F",mktime(0,0,0,$curMonth,1,$curYear));
	$firstDayOfMonth = date("w",mktime(0,0,0,$curMonth,1,$curYear));
	echo "<table cellpadding=\"3\" cellspacing=\"1\" bgcolor=\"#000000\" align=\"center\">\r";
	echo "<tr><td class=\"month\" colspan=\"7\">$monthTextual - $curYear</td></tr>\r";
	if ($firstDayOfMonth > 0) { echo "<tr>\r"; }
	for($cellCount=0;$cellCount<=$firstDayOfMonth-1;$cellCount++)
	{
		echo "<td class=\"day\"> </td>\r";
	}
	for ($curDay=1;$curDay<=$totalDays;$curDay++)
	{
		if ($cellCount == 0) { echo "<tr>\r"; }
		echo "<td class=\"day\" id=\"$curMonth-$curDay\" onMouseOver=\"changeBG('$curMonth-$curDay','over');\" onMouseOut=\"changeBG('$curMonth-$curDay','out');\">$curDay</td>\r";
		$cellCount++;
		if ($cellCount == 7) { echo "</tr>\r"; $cellCount=0;}
	}
	if ($cellCount > 0 && $cellCount < 7)
	{
		for ($i=$cellCount; $i<7; $i++)
		{
			echo "<td class=\"day\"> </td>\r";
		}
		echo "</tr>\r";
	}
	echo "</table><br>\r";
	$mainTableCellCount++;
	if ($mainTableCellCount == 3) { echo "</tr>\r"; $mainTableCellCount = 0; }
}
echo "<form action=\"$PHP_SELF\" method=\"GET\">\r";
echo "<select name=\"curYear\">\r";
for($yearOffset=-4;$yearOffset<=4;$yearOffset++)
{
	$year = date("Y", mktime(0,0,0,0,0,date("Y")+$yearOffset));
	if ($year == $curYear) { $selected = " selected"; } else { $selected = ""; }
	echo "<option value=\"$year\"$selected>$year</option>\r";
}
echo "</select>\r";
echo "<input type=\"Submit\" value=\"Submit\">\r";
echo "</form>\r";
?>
```

