<div align="center">

## hits counter


</div>

### Description

it's a simple hit counter which keeps track your visitor to the site ,it also keeps count of the perticular ip and its count,it also keeps the last visited page
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[sandeep choudhury](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/sandeep-choudhury.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__8-1.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/sandeep-choudhury-hits-counter__8-293/archive/master.zip)





### Source Code

```
<?
  ## before using this code you must make the following table in your database
  #  Table name: stats
  # fields: Ipaddress(varchar(150)),host(varchar(150)),browser(varchar(150)),referer(varchar(150)),filename(varchar(150)).
  # table name: hits
  # fields: ipaddress(varchar(150)),count(int(11))
  ###############################################
  global $dblink,$PHP_SELF;
  $ip = getenv("REMOTE_ADDR");
  $host = getenv("HTTP_HOST");
  $browser = getenv("HTTP_USER_AGENT");
  $referer = getenv("HTTP_REFERER");
  $sql = "SELECT ipaddress FROM stats WHERE ipaddress = '$ip'";
  #### TO DO ######################
	# make the connection to your database here
	$result = @mysql_query($sql, $dblink);
  $num = mysql_num_rows($result);
	if( $num == 0 )
  {
	$sql ="INSERT INTO stats(ipaddress,host,browser,referer,filename) VALUES('$ip', '$host', '$browser', '$referer','$PHP_SELF')";
	$result=mysql_query($sql,$dblink);
	$sql1="INSERT INTO hits(ipaddress,count) VALUES('$ip',1)";
	$result1=@mysql_query($sql1,$dblink);
	$text="you had a new visitor from IP: $ip, Host: $host Browser: $browser Referer: $referer";
	 if ($result)
		{
		mail("abc@abc.com", "You had a new visitor",$text, "FROM: stats@abc.com");
		}
	}else{
	$sql = "UPDATE hits SET count = count + 1 where ipaddress='$ip'";
	$result =@mysql_query($sql, $dblink) ;
	$sql2 = "UPDATE stats SET filename ='$PHP_SELF' where ipaddress='$ip'";
	$result2 =@mysql_query($sql2, $dblink) ;
  }
?>
```

