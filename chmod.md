In UNIX based systems, there are 3 types of owners (U or G or O) of a file (<a href="https://en.wikipedia.org/wiki/Everything_is_a_file">Everything in Linux is a file!</a>)


<b>User (U)</b> - The user is also the owner of the file. The creator of the files becomes the owner of the file.


<b>Group (G)</b> - A group can contain multiple users. All the users in the group will have the same type of permissions or access.


<b>Other (O)</b> - All the other users who have access to the file.  


So, when ever we see chmod we are always seeing this format of results, mainly:

fUUUGGGOOO or dUUUGGGOOO 

total of 10 bits. Can be represented as: - - - - - - - - - -

<br>
 <p><b><font color="white">Permissions:</font></b></p>

We talked about the owners of the file above. Different types of owners (U, G, or O) have different types of permissions/access (R or W or X):

<b>Read (R)</b>: read permission gives you the ability to open and read a file. The read permission on a directory means that we have access to list the directory.

<b>Write (W)</b>: write permission gives you the authority of modifying the contents of the file. Write permission on a directory gives you the permission to add, delete or rename files in the directory. 

<b>Execute (X)</b>

 In Unix based systems, you cannot run a file unless the execute (X) permissoin is set. If the X is not set, you might still be able to view the program code(provided read & write permissions are set), but not run it. (just like .exe executable in Windows!)

For example, lets understand what the following modes mean and how they are calculated:

<!--

<!--Explain how and why it is calculated -->

<table> <!--#----------------Headings------------ -->
  <th></th>
  <th>Read. (R)</th>
  <th>Write (W)</th>
  <th>Execute (X)</th>

  <!---------Table data for table rows------------->

  <tr> <!---------Row 1------------->
    <td><b>User (U)</b></td>

    <td>
      <input type="checkbox" id="User-Read" name="User-Read" value="4"><label for="User-Read"></label>
    </td>

    <td>
      <input type="checkbox" id="User-Write" name="User-Write" value="2"><label for="User-Write"></label>
    </td>

    <td>
      <input type="checkbox" id="User-Execute" name="User-Execute" value="1"><label for="User-Execute"></label>
    </td>
  </tr>
    

  <tr> <!---------Row 2------------->
    <td><b>Group (G)</b></td>

    <td>
      <input type="checkbox" id="Group-Read" name="Group-Read" value="4">
      <label for="Group-Read"></label>
    </td>

    <td>
      <input type="checkbox" id="Group-Write" name="Group-Write" value="2">
      <label for="Group-Write"></label>
    </td>

    <td>
      <input type="checkbox" id="Group-Execute" name="Group-Execute" value="1">
      <label for="Group-Execute"></label>
    </td>
  </tr>
    

  <tr> <!---------Row 3------------->
    <td><b>Other (O)</b></td>

    <td>
      <input type="checkbox" id="Group-Read" name="Group-Read" value="4"><label for="Group-Read"></label>
    </td>

    <td>
        <input type="checkbox" id="Group-Write" name="Group-Write" value="2"><label for="Group-Write"></label>
    </td>

    <td>
        <input type="checkbox" id="Group-Execute" name="Group-Execute" value="1"><label for="Group-Execute"></label>
    </td>
</tr>  
</table>


-->


<script type="text/javascript">
<!--

/*
Jeroen's Chmod Calculator- By Jeroen Vermeulen of Alphamega Hosting <jeroen@alphamegahosting.com> 
Visit http://www.javascriptkit.com for this script and more
This notice must stay intact
*/
 
function octalchange() 
{
	var val = document.chmod.t_total.value;
	var ownerbin = parseInt(val.charAt(0)).toString(2);
	while (ownerbin.length<3) { ownerbin="0"+ownerbin; };
	var groupbin = parseInt(val.charAt(1)).toString(2);
	while (groupbin.length<3) { groupbin="0"+groupbin; };
	var otherbin = parseInt(val.charAt(2)).toString(2);
	while (otherbin.length<3) { otherbin="0"+otherbin; };
	document.chmod.owner4.checked = parseInt(ownerbin.charAt(0)); 
	document.chmod.owner2.checked = parseInt(ownerbin.charAt(1));
	document.chmod.owner1.checked = parseInt(ownerbin.charAt(2));
	document.chmod.group4.checked = parseInt(groupbin.charAt(0)); 
	document.chmod.group2.checked = parseInt(groupbin.charAt(1));
	document.chmod.group1.checked = parseInt(groupbin.charAt(2));
	document.chmod.other4.checked = parseInt(otherbin.charAt(0)); 
	document.chmod.other2.checked = parseInt(otherbin.charAt(1));
	document.chmod.other1.checked = parseInt(otherbin.charAt(2));
	calc_chmod(1);
};

function calc_chmod(nototals)
{
  var users = new Array("owner", "group", "other");
  var totals = new Array("","","");
  var syms = new Array("","","");

	for (var i=0; i<users.length; i++)
	{
	  var user=users[i];
		var field4 = user + "4";
		var field2 = user + "2";
		var field1 = user + "1";
		//var total = "t_" + user;
		var symbolic = "sym_" + user;
		var number = 0;
		var sym_string = "";
	
		if (document.chmod[field4].checked == true) { number += 4; }
		if (document.chmod[field2].checked == true) { number += 2; }
		if (document.chmod[field1].checked == true) { number += 1; }
	
		if (document.chmod[field4].checked == true) {
			sym_string += "r";
		} else {
			sym_string += "-";
		}
		if (document.chmod[field2].checked == true) {
			sym_string += "w";
		} else {
			sym_string += "-";
		}
		if (document.chmod[field1].checked == true) {
			sym_string += "x";
		} else {
			sym_string += "-";
		}
	
		//if (number == 0) { number = ""; }
	  //document.chmod[total].value = 
		totals[i] = totals[i]+number;
		syms[i] =  syms[i]+sym_string;
	
  };
	if (!nototals) document.chmod.t_total.value = totals[0] + totals[1] + totals[2];
	document.chmod.sym_total.value = "-" + syms[0] + syms[1] + syms[2];
}
window.onload=octalchange
//-->
</script>

<form name="chmod">
<TABLE BORDER="0" CELLSPACING="0" CELLPADDING="0" style="font:normal 12px Verdana";>
<TR ALIGN="LEFT" VALIGN="MIDDLE">
<TD>Permissions: </TD>
<TD><input type="text" name="t_total" value="751" size="4" onKeyUp="octalchange()"> </TD>
<TD><input type="text" name="sym_total" value="" size="12" READONLY="1" STYLE='border: 0px none; font-family: "Courier New", Courier, mono;'></TD>
</TR>
</TABLE>
<BR>
<table cellpadding="2" cellspacing="0" border="0" style="font:normal 12px Verdana">
<tr bgcolor="#333333">
<td WIDTH="60" align="left"> </td>
<td WIDTH="55" align="center" style="color:white"><b>owner
</b></td>
<td WIDTH="55" align="center" style="color:white"><b>group
</b></td>
<td WIDTH="55" align="center" style="color:white"><b>other
<b></td>
</tr>
<tr bgcolor="#dddddd">
<td WIDTH="60" align="left" nowrap BGCOLOR="#FFFFFF">read</td>
<td WIDTH="55" align="center" bgcolor="#EEEEEE">
<input type="checkbox" name="owner4" value="4" onclick="calc_chmod()">
</td>
<td WIDTH="55" align="center" bgcolor="#ffffff"><input type="checkbox" name="group4" value="4" onclick="calc_chmod()">
</td>
<td WIDTH="55" align="center" bgcolor="#EEEEEE">
<input type="checkbox" name="other4" value="4" onclick="calc_chmod()">
</td>
</tr>
<tr bgcolor="#dddddd">		
<td WIDTH="60" align="left" nowrap BGCOLOR="#FFFFFF">write</td>
<td WIDTH="55" align="center" bgcolor="#EEEEEE">
<input type="checkbox" name="owner2" value="2" onclick="calc_chmod()"></td>
<td WIDTH="55" align="center" bgcolor="#ffffff"><input type="checkbox" name="group2" value="2" onclick="calc_chmod()">
</td>
<td WIDTH="55" align="center" bgcolor="#EEEEEE">
<input type="checkbox" name="other2" value="2" onclick="calc_chmod()">
</td>
</tr>
<tr bgcolor="#dddddd">		
<td WIDTH="60" align="left" nowrap BGCOLOR="#FFFFFF">execute</td>
<td WIDTH="55" align="center" bgcolor="#EEEEEE">
<input type="checkbox" name="owner1" value="1" onclick="calc_chmod()">
</td>
<td WIDTH="55" align="center" bgcolor="#ffffff"><input type="checkbox" name="group1" value="1" onclick="calc_chmod()">
</td>
<td WIDTH="55" align="center" bgcolor="#EEEEEE">
<input type="checkbox" name="other1" value="1" onclick="calc_chmod()">
</td>
</tr>
</table>
<span style="font:normal 11px Arial">This free JavaScript provided by <a href="http://www.javascriptkit.com">JavaScript Kit</a></span>
</form>

<br>
