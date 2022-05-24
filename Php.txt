
Assignment 1: Cookies and Session
Set A
1.Write a php script to keep track of numbers of times the web page has been access.[use session and cookies]
Using Session
<?php
	session_start();
	if(isset($_SESSION['count']))
	{
		$_SESSION['count']+=1;
		echo "You have visited this page ".$_SESSION['count']. " times";
	}
	else
	{
		$_SESSION['count']=1;
		echo "You have visited this page {$_SESSION['count']} times";
	}
?>

Using cookies
<?php
	If(isset($_COOKIE[‘cnt’]))
	{
		$x=$_COOKIE[‘cnt’];
		$x=$x+1;
		Setcookie(‘cnt’,$x);
	}
	else
	{
		setcookie(‘cnt’,2);
		echo”you havev accessed this page 1st time”;
	}
	echo”you havev accessed this page $x times”;
?>

2 Write a PHP script to change the preference of your web page like font style, font, size, font color, background color using cookie.
Display selected settings on next page and actual implementation ( with new settings) on third page.

HTML file :

<html>
<body>
<form action="slip21_2_1.php" method="get">
<center>
<b>Select font style :</b><input type=text name=s1> <br>
<b>Enter font size : </b><input type=text name=s><br>
<b>Enter font color : </b><input type=text name=c><br>
<b>Enter background color :</b> <input type=text name=b><br>
<input type=submit value="Next">
</center>
</form>
</body>
</html>

PHP file 

<?php
echo "style is ".$_GET['s1']."<br>color is ".$_GET['c']."<br>Background color is ".$_GET['b']."<br>size is ".$_GET['s'];
setcookie("set1",$_GET['s1'],time()+3600);
setcookie("set2",$_GET['c'],time()+3600);
setcookie("set3",$_GET['b'],time()+3600);
setcookie("set4",$_GET['s'],time()+3600);
?>

<html>
<body>
<form action="slip21_2_2.php">
<input type=submit value=OK>
</form>
</body>
</html>

PHP file : slip21_2_2.php
<?php
$style = $_COOKIE['set1'];
$color = $_COOKIE['set2'];
$size = $_COOKIE['set4'];
$b_color = $_COOKIE['set3'];
$msg = "NR Classes";
echo "<body bgcolor=$b_color>";
echo "<font color=$color size=$size>$msg";
echo "</font></body>";
?>

Set B
1 Write a PHP script to accept username and password. If in the first three chances, username and password entered is correct then display second form with ‘welcome message’ otherwise display error message. [ Use Session]

HTML file :

<html>
<head>
<script>
                function getans()
                {
                                st1=document.getElementById('txtname').value;
                                st2=document.getElementById('txtpass').value;
                                ob=new XMLHttpRequest();
             
                                ob.onreadystatechange=function()
                                {
                                                if(ob.readyState==4 && ob.status==200)
                                                {
                                                                if(ob.responseText==3)
                                                                {
                                                                                alert("sorry you lost the chances to login");
                                                                                location="error.html";
                                                                }
                                                                else if(ob.responseText=="correct")
                                                                {
                                                                                alert("you entered correct details");
                                                                }
                                                                else alert(ob.responseText);   
                                                }                                           
                                }           
                                ob.open("GET","slip8_Q2.php?n="+st1+"&p="+st2);
                                ob.send();
                }
</script>
</head>
<body>
<input type=text id=txtname placeholder="username"></br>
<input type=password id=txtpass placeholder="password"></br>
<input type="button" onclick="getans()" value="Login">

</body>
</html>

HTML file :

<html>
<body>
<h1>YOu lossed the chances of login</h1>
</body>
</html>

PHP file :
<?php
                session_start();
                $nm=$_GET['n'];
                $ps=$_GET['p'];
                if($nm==$ps)
                {
                                echo "correct";
                }
                else if(isset($_SESSION['cnt']))
                                                {
                                                                $x=$_SESSION['cnt'];
                                                                $x=$x+1;
                                                                $_SESSION['cnt']=$x;
                                                                echo $_SESSION['cnt'];
                                                             
                                                                if($_SESSION['cnt']>=3)
                                                                $_SESSION['cnt']=1;
                                                }
                                                else
                                                {
                                                                $_SESSION['cnt']=1;
                                                                echo "1";
                                                }
?>

2Write a PHP script to accept Employee details ( Eno, Ename, address) on first page. On second page accept earning( Basic, Da, HRA). On third page print Employee information( ENO,Ename, Address, BASIC, DA, HRA, TOTAL)
[Hint:Use Session]
HTML file :

<html>
<body>
<form action="slip18_2_1.php" method="get">
<center>  <h2>Enter Enployee Details :</h2>  <br>

<table>
<tr>  <td><b>Emp no :</b></td>            <td><input type=text name=eno></td>        </tr>
<tr>  <td><b> Name :</b></td>             <td><input type=text name=enm></td>        </tr>
<tr>  <td><b>Address :</b></td>                      <td><input type=text name=eadd></td>        </tr>
</table>
<br>  <input type=submit value=Show name=submit>
</center>
</form>
</body>
</html>

PHP file : 

<?php
session_start();
$eno = $_GET['eno'];
$enm = $_GET['enm'];
$eadd = $_GET['eadd'];

$_SESSION['eno'] = $eno;
$_SESSION['enm'] = $enm;
$_SESSION['eadd'] = $eadd;
?>

<html>
<body>

<form action="slip18_2_2.php" method="post">
<center>
<h2>Enter Earnings of Employee:</h2>

<table>
<tr><td>Basic : </td><td><input type="text" name="e1"></td><tr>
<tr><td>DA : </td><td><input type="text" name="e2"></td></tr>
<tr><td>HRA : </td><td><input type="text" name="e3"></td></tr>
<tr><td></td><td><input type="submit" value=Next></td></tr>
</table>
</center>
</form>
</body>
</html>

PHP file :
<?php
session_start();
$e1 = $_POST['e1'];
$e2 = $_POST['e2'];
$e3= $_POST['e3'];

echo "<h3>Employee Details</h3> ";
echo "Name : ".$_SESSION['eno']."<br>";
echo "Address : ".$_SESSION['enm']."<br>";
echo "Class : ".$_SESSION['eadd']."<br><br>";

echo "basic : ".$e1."<br>";
echo "DA : ".$e2."<br>";
echo "HRA : ".$e3."<br>";

$total = $e1+$e2+$e3;
echo "<h2>Total Of Earnings Is : ".$total."</h2>";
?>

Set C
1.Create a form to accept customer information (name, address, ph-no). Once the customer information is accepted, accept product information in the next form (Product name, qty, rate). Display the bill for the customer in the next form. Bill should contain the customer information and the information of the products entered
PHP File
<?php
session_start();
	$_SESSION['cname']=$_POST['cname'];
	$_SESSION['caddr']=$_POST['caddr'];
	$_SESSION['cmono']=$_POST['cmono'];
?>

<html>
	<body>
		<form action="c1_2.php" method="POST">
			Product Name: <input type="text" name="ProdName">
			Quantity: <input type="text" name="qty">
			Rate: <input type="text" name="rate">
			<input type="submit" value="submit">
		</form>
	</body>
</html>

PHP File
<?php
session_start();
	$_SESSION['ProdName']=$_POST['ProdName'];
	$_SESSION['qty']=$_POST['qty'];
	$_SESSION['rate']=$_POST['rate'];
	
	$_amount=$_SESSION['rate']*$_SESSION['qty'];
	
	echo "<br> Customer name:".$_SESSION['cname']. "<br> Customer address:".$_SESSION['caddr']. "<br> Customer Mob no:".$_SESSION['cmono']."<br> Product name:".$_SESSION['ProdName']."<br> Rate:".$_SESSION['rate']. "<br> Quantity:".$_SESSION['qty']. "<br> Amount:".$_amount;

session_destroy();


Assignment2:XML Documents and Dom 

1Write a script to create XMLfile named “Item.xml”
<Item>
	<ItemName>………………</ItemName>
	<ItemPrice>………………..</ItemPrice>
	<Quantity>………………….</Quantity>
</Item>

PHP File:
<?php
$xmlgen='<?xml version="1.0" encoding="UTF-8" ?>';
$xmldoc=new SimpleXMLElement("<Shop></Shop>");

$item1 = $xmldoc->addChild('Item');
$item1->addChild('ItemName', 'Rorito Pen');
$item1->addChild('ItemPrice', 50);
$item1->addChild('Quantity', 1000);

$item2 = $xmldoc->addChild('Item');
$item2->addChild('ItemName', 'Natraj Pencil');
$item2->addChild('ItemPrice', 25);
$item2->addChild('Quantity', 200);

$item3 = $xmldoc->addChild('Item');
$item3->addChild('ItemName', 'Camlin Eraser');
$item3->addChild('ItemPrice', 60);
$item3->addChild('Quantity', 500);

$item4 = $xmldoc->addChild('Item');
$item4->addChild('ItemName', 'Classmate Notebook');
$item4->addChild('ItemPrice', 60);
$item4->addChild('Quantity', 1200);

$item5 = $xmldoc->addChild('Item');
$item5->addChild('ItemName', 'Maped Rounder');
$item5->addChild('ItemPrice', 120);
$item5->addChild('Quantity', 1400);
$xmldoc->asXML('item.xml');

?>

XML File:
 <?xml version="1.0"?>
<?xml-stylesheet type="text/css" href="item.css"?>
<Shop>
<Item>
<ItemName>Pen</ItemName><ItemPrice>50</ItemPrice><Quantity>1000</Quantity></Item>
<Item>
<ItemName>Natraj Pencil</ItemName><ItemPrice>25</ItemPrice><Quantity>200</Quantity></Item>
<Item>
<ItemName>Camlin Eraser</ItemName><ItemPrice>60</ItemPrice><Quantity>500</Quantity></Item>
<Item>
<ItemName>Classmate Notebook</ItemName><ItemPrice>60</ItemPrice><Quantity>1200</Quantity></Item>
<Item>
<ItemName>Maped Rounder</ItemName><ItemPrice>120</ItemPrice><Quantity>1400</Quantity></Item></Shop> 

2 link item.xml file to the CSS stylesheet and get well formatted output as a given below
1	ItemName
		Color:red;
		Font-Family:copperplate Gothic Light;
		Font-Size:16pt;
		Font:bold

2	ItemPrice and Quantity
		Color:yellow;
		Font-Family:Arial;
		Font-Size:12pt;
		Font:bold
XML File:

<?xml version="1.0"?>
<?xml-stylesheet type="text/css" href="item.css"?>
<Shop><Item><ItemName>Rorito Pen</ItemName><ItemPrice>50</ItemPrice><Quantity>1000</Quantity></Item><Item><ItemName>Natraj Pencil</ItemName><ItemPrice>25</ItemPrice><Quantity>200</Quantity></Item><Item><ItemName>Camlin Eraser</ItemName><ItemPrice>60</ItemPrice><Quantity>500</Quantity></Item><Item><ItemName>Classmate Notebook</ItemName><ItemPrice>60</ItemPrice><Quantity>1200</Quantity></Item><Item><ItemName>Maped Rounder</ItemName><ItemPrice>120</ItemPrice><Quantity>1400</Quantity></Item></Shop>

CSS File:
ItemName {
  color: red;
  font-family: Copperplate Gothic Light;
  font-size: 16pt;
  font: bold;
}

ItemPrice {
  color: yellow;
  font-family: Arial;
  font-size: 12pt;
  font: bold;
}

Quantity {
  color: blue;
  font-family: Arial;
  font-size: 12pt;
  font: bold;

PHP File:
<?php
$xmlgen='<?xml version="1.0" encoding="UTF-8" ?>';
$xmldoc=new SimpleXMLElement("<Shop></Shop>");

$item1 = $xmldoc->addChild('Item');
$item1->addChild('ItemName', 'Rorito Pen');
$item1->addChild('ItemPrice', 50);
$item1->addChild('Quantity', 1000);

$item2 = $xmldoc->addChild('Item');
$item2->addChild('ItemName', 'Natraj Pencil');
$item2->addChild('ItemPrice', 25);
$item2->addChild('Quantity', 200);

$item3 = $xmldoc->addChild('Item');
$item3->addChild('ItemName', 'Camlin Eraser');
$item3->addChild('ItemPrice', 60);
$item3->addChild('Quantity', 500);

$item4 = $xmldoc->addChild('Item');
$item4->addChild('ItemName', 'Classmate Notebook');
$item4->addChild('ItemPrice', 60);
$item4->addChild('Quantity', 1200);

$item5 = $xmldoc->addChild('Item');
$item5->addChild('ItemName', 'Maped Rounder');
$item5->addChild('ItemPrice', 120);
$item5->addChild('Quantity', 1400);
$xmldoc->asXML('item.xml');

?>

3Write a PHP script to generate an XML in the following format in php.

XML File:
<?xml version="1.0" encoding="UTF-8"?>
<BookInfo>
  <book category="Project">
    <bookno>1</bookno>
    <bookname>JAVA</bookname>
    <author>Balguru Swami</author>
    <price>250</price>
    <year>2006</year>
  </book>
  <book category="Assembly">
    <bookno>2</bookno>
    <bookname>c</bookname>
    <author>Dennis Ritchie</author>
    <price>500</price>
    <year>1971</year>
  </book>
</BookInfo>

PHP File:
<?php
	$doc=new DOMDocument("1.0", "UTF-8");
	$doc->formatOutput=true;
	$bookinfo=$doc->createElement("BookInfo");
	$doc->appendChild($bookinfo);
	$book=$doc->createElement("book");
	$bookinfo->appendChild($book);
	$no=$doc->createElement("bookno", "1");
	$book->appendChild($no);
	$name=$doc->createElement("bookname", "JAVA");
	$book->appendChild($name);
	$author=$doc->createElement("author", "Balguru Swami");
	$book->appendChild($author);
	$price=$doc->createElement("price", "250");
	$book->appendChild($price);
	$year=$doc->createElement("year", "2006");
	$book->appendChild($year);
	
						
	$book1=$doc->createElement("book");
	$bookinfo->appendChild($book1);
	$no1=$doc->createElement("bookno", "2");
	$book1->appendChild($no1);
	$name1=$doc->createElement("bookname", "c");
	$book1->appendChild($name1);
	$author1=$doc->createElement("author", "Dennis Ritchie");
	$book1->appendChild($author1);
	$price1=$doc->createElement("price", "500");
	$book1->appendChild($price1);
	$year1=$doc->createElement("year", "1971");
	$book1->appendChild($year1);
		
	$doc->save("book.xml");
	echo "book.xml created";
?>

Set B
1write a PHP script to read above created book.xml file into simple XML object. display attributes and elements 
[Hint L simple_XML_load_ file() function]

XML File:
<?xml version="1.0" encoding="UTF-8"?>
<BookInfo>
  <book category="Project">
    <bookno>1</bookno>
    <bookname>JAVA</bookname>
    <author>Balguru Swami</author>
    <price>250</price>
    <year>2006</year>
  </book>
  <book category="Assembly">
    <bookno>2</bookno>
    <bookname>c</bookname>
    <author>Dennis Ritchie</author>
    <price>500</price>
    <year>1971</year>
  </book>
</BookInfo>

PHP File:
<?php
	$doc=new DOMDocument("1.0", "UTF-8");
	$doc->formatOutput=true;
	$bookinfo=$doc->createElement("BookInfo");
	$doc->appendChild($bookinfo);
	$book=$doc->createElement("book");
	$bookinfo->appendChild($book);
	$no=$doc->createElement("bookno", "1");
	$book->appendChild($no);
	$name=$doc->createElement("bookname", "JAVA");
	$book->appendChild($name);
	$author=$doc->createElement("author", "Balguru Swami");
	$book->appendChild($author);
	$price=$doc->createElement("price", "250");
	$book->appendChild($price);
	$year=$doc->createElement("year", "2006");
	$book->appendChild($year);
	
						
	$book1=$doc->createElement("book");
	$bookinfo->appendChild($book1);
	$no1=$doc->createElement("bookno", "2");
	$book1->appendChild($no1);
	$name1=$doc->createElement("bookname", "c");
	$book1->appendChild($name1);
	$author1=$doc->createElement("author", "Dennis Ritchie");
	$book1->appendChild($author1);
	$price1=$doc->createElement("price", "500");
	$book1->appendChild($price1);
	$year1=$doc->createElement("year", "1971");
	$book1->appendChild($year1);
		
	$doc->save("book.xml");
	echo "book.xml created";
?>

PHP File:
<?php
	$stocklist=simplexml_load_file("book.xml") or die ("Error");
	foreach($stocklist->book as $books)
	{
		echo "<br>Book category attribute: ".$books->attributes()."<br>";
		echo "<br>Book number: ".$books->bookno."<br>";
		echo "<br>Book name: ".$books->bookname."<br>";
		echo "<br>Book author: ".$books->author."<br>";
		echo "<br>Book price: ".$books->price."<br>";
		echo "<br>Book published year: ".$books->year."<br>";
	}	
?>

2 write a PHP script to read “movie.xml” file and print all movie title and actor name of file using domdocument Paser. “movie.xml” file should contain following information with at least 5 records with values.
 MovieInfo
 MovieNo, MovieTitle, ActorName,ReleaseYear

XML File:
<?xml version="1.0" encoding="UTF-8"?>
<Movie>
  <category type="Classic">
    <MovieTitle>KGF</MovieTitle>
    <ActorName>Anand</ActorName>
    <ReleaseYear>2018</ReleaseYear>
  </category>
  <category type="Classic">
    <MovieTitle>Bean</MovieTitle>
    <ActorName>Rowan</ActorName>
    <ReleaseYear>1998</ReleaseYear>
  </category>
  <category type="Horror">
    <MovieTitle>Annabelle</MovieTitle>
    <ActorName>Hannah</ActorName>
    <ReleaseYear>2015</ReleaseYear>
  </category>
  <category type="Horror">
    <MovieTitle>Get Out</MovieTitle>
    <ActorName>Daniel</ActorName>
    <ReleaseYear>2014</ReleaseYear>
  </category>
  <category type="Action">
    <MovieTitle>The Batman</MovieTitle>
    <ActorName>Robert</ActorName>
    <ReleaseYear>2022</ReleaseYear>
  </category>
</Movie>

PHP File:
<?php
$dom=new DomDocument();
$dom->load("movie.xml");
echo"<h2>Name of Movie</h2>";
$mname=$dom->getElementsByTagName("MovieTitle");
foreach($mname as $m){
	echo"$m->textContent<br><br>";
}

echo"<h2>Movie Actor Name</h2>";
$mname=$dom->getElementsByTagName("ActorName");
foreach($mname as $b){
	echo"$b->textContent<br><br>";
}



?>

Set C
1

<?php	
	$doc=new DOMDocument("1.0", "UTF-8");
	$doc->formatOutput=true;

	$movie=$doc->createElement("Movie");
	$doc->appendChild($movie);

	$category=$doc->createElement("category");
	$category->setAttribute("type", "Classic");
	$movie->appendChild($category);
	

	$movie_title=$doc->createElement("MovieTitle", "KGF");
	$category->appendChild($movie_title);
	$Actor_name=$doc->createElement("ActorName", "Anand");
	$category->appendChild($Actor_name);
	$year=$doc->createElement("ReleaseYear", "2018");
	$category->appendChild($year);

	$category=$doc->createElement("category");
	$category->setAttribute("type", "Classic");
	$movie->appendChild($category);
	

	$movie_title=$doc->createElement("MovieTitle", "Bean");
	$category->appendChild($movie_title);
	$Actor_name=$doc->createElement("ActorName", "Rowan");
	$category->appendChild($Actor_name);
	$year=$doc->createElement("ReleaseYear", "1998");
	$category->appendChild($year);

	$category=$doc->createElement("category");
	$category->setAttribute("type", "Horror");
	$movie->appendChild($category);
	

	$movie_title=$doc->createElement("MovieTitle", "Annabelle");
	$category->appendChild($movie_title);
	$Actor_name=$doc->createElement("ActorName", "Hannah");
	$category->appendChild($Actor_name);
	$year=$doc->createElement("ReleaseYear", "2015");
	$category->appendChild($year);

	$category=$doc->createElement("category");
	$category->setAttribute("type", "Horror");
	$movie->appendChild($category);
	

	$movie_title=$doc->createElement("MovieTitle", "Get Out");
	$category->appendChild($movie_title);
	$Actor_name=$doc->createElement("ActorName", "Daniel");
	$category->appendChild($Actor_name);
	$year=$doc->createElement("ReleaseYear", "2014");
	$category->appendChild($year);

	$category=$doc->createElement("category");
	$category->setAttribute("type", "Action");
	$movie->appendChild($category);
	

	$movie_title=$doc->createElement("MovieTitle", "The Batman");
	$category->appendChild($movie_title);
	$Actor_name=$doc->createElement("ActorName", "Robert");
	$category->appendChild($Actor_name);
	$year=$doc->createElement("ReleaseYear", "2022");
	$category->appendChild($year);

	$doc->save("movie.xml");
	echo "movie.xml created";
?>

XML File:
<?xml version="1.0" encoding="UTF-8"?>
<Movie>
  <category type="Classic">
    <MovieTitle>KGF</MovieTitle>
    <ActorName>Anand</ActorName>
    <ReleaseYear>2018</ReleaseYear>
  </category>
  <category type="Classic">
    <MovieTitle>Bean</MovieTitle>
    <ActorName>Rowan</ActorName>
    <ReleaseYear>1998</ReleaseYear>
  </category>
  <category type="Horror">
    <MovieTitle>Annabelle</MovieTitle>
    <ActorName>Hannah</ActorName>
    <ReleaseYear>2015</ReleaseYear>
  </category>
  <category type="Horror">
    <MovieTitle>Get Out</MovieTitle>
    <ActorName>Daniel</ActorName>
    <ReleaseYear>2014</ReleaseYear>
  </category>
  <category type="Action">
    <MovieTitle>The Batman</MovieTitle>
    <ActorName>Robert</ActorName>
    <ReleaseYear>2022</ReleaseYear>
  </category>
</Movie>

PHP File:
<?php
$dom=new DomDocument();
$dom->load("movie.xml");
echo"<h2>Name of Movie</h2>";
$mname=$dom->getElementsByTagName("MovieTitle");
foreach($mname as $m){
	echo"$m->textContent<br><br>";
}

echo"<h2>Movie Actor Name</h2>";
$mname=$dom->getElementsByTagName("ActorName");
foreach($mname as $b){
	echo"$b->textContent<br><br>";
}



?>

Assignment3: Java Script And Jquery

Set A

1 write a JavaScript to display message ‘Exam are near,you have started preparing for?’using alert,from and confirm boxes. accept proper input from user and display message accordingly.

HTML & JAVA Script File:
<html>
	<head>
		
<script language="javascript">
			
function show_prompt()
			
{
				
let person=prompt("Please enter your name", "Arya");
				
if(person!=null)
					
document.getElementById("demo").innerHTML="Hello "+person+"! How are you?";	
			}
			
			
function show_confirm()
			
{
				
var r=confirm("Exams are near, have you started preparing for them?");
				
if(r==true)
					
x="You pressed OKAY!";
				
else
					
x="You pressed CANCEL!";
			
}

			
function show_alert()
			
{
				
alert("Exams are near, have you started preparing for them?");	
			
}
		
</script>
	</head>

	<body>
		
<button onclick="show_prompt()">Prompt</button>

		
<p id="demo"></p>
<input type="button" onclick="show_confirm()" value="Show confirm">
		
<input type="button" onclick="show_alert()" value="Show alert">

	
</body>
</html>


2 Add or append in paragraph text and also in the numbered ordered list in a given HTML document using jQuery selectors.
[Hint:Use before() and after()]



HTML & JAVA Script File:
<html>
	<head>
		<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
		<script>
		
	
		var person = prompt("Please enter list element", "List Item ");
		var person1 = prompt("Please enter data for paragraph", "List Item ");
  				
		
		$(document).ready(function()
		{
      			$("#button1").click(function()
			{
	         		$("p").append("<b>" + person1+"</b>");
	       		});

 	     		$("#button2").click(function()
			{
        	 		$("ol").append("<li>"+person+"</li>");
       			});
 		 });
		</script>	
	</head>
	<body>
  		<p>Paragraph </P>
  		<ol>
			<h3>List is as follows: </h3>
    				<li>Sugar</li>
    				<li>Salt</li>
  		</ol>

		<button id = "button1">Append in paragraph</button>
		<button id = "button2">Append in list </button>
	</body>
</html>



<input type="button" onclick="show_confirm()" value="Show confirm">
		
<input type="button" onclick="show_alert()" value="Show alert">

	
</body>
</html>


Set B
1write a JavaScript function to validate username and password for name membership form.

HTML & JAVA Script File:
<!DOCTYPE html>
<html>
 		<script type = "text/javascript">  
    			function validateform()
			{  
    				var n = document.myform.n.value;  
    				var p = document.myform.p.value; 
				console.log(n);
				console.log(p); 
      
    				if(n == null || p == null || p.length<6)
				{  
      					alert("Error"); 
      					return false;  
    				}  
     				else
      					alert("Registered successfully!");
    			}  
    		</script>
	<body>  
    		<form name="myform" onsubmit="return validateform()">  
    			Name: <input type="text" name="n"><br/>  
    			Password: <input type="password" name="p"><br/>  
    			<input type="submit" value="Register">  
    		</form>  
    	</body>
</html>


2 To insert text before and after an image using jQuery 
[Hint: use before() and after()]

HTML & JAVA Script File:

<!DOCTYPE html>
<html>
	<head>
		<script src = "https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
		<script>
			$(document).ready(function()
			{
       				$("#button1").click(function()
				{
					$("img").before("<b>Nature     </b>");
				});

	 			$("#button2").click(function()
				{
	 				$("img").after("<b>     Nature</b>");
	 			});
	 		});

		</script>
		</head>
	<body>
		<img src="image.jpg" width="500" height="400"> 
		<br><button id = "button1">Add text before</button>
		<button id = "button2">Add text after</button>
	</body>
</html>
Set C
1 write a JavaScript program to accept name of student, change font colour to Red, font size to 18 if student name is present otherwise on clicking on empty textbox display image which changes its size (use onblur, onload, onmouseover, onMouseclick, onMouseup)

HTML & JAVA Script File:
<!DOCTYPE html>
<html>
	<body>
 		<script type = "text/javascript">
  			function myFunction()
  			{
      				var x=document.getElementById("pass").value;
      				if(x!=null && x!="")
      				{
					document.getElementById("pass").style.color="red";
					document.getElementById("pass").fontsize="18px";
        				document.write(x.fontcolor("red") && x.font.size("18px"))
      				}
      				else
      				{
					document.getElementById("myImg").height="400";
 					document.getElementById("myImg").width="400";
      				}
 			}
 		</script>

		<img align="center" src="image.jpg" width="300" height="300" id="myImg"> 
		Enter Student Name<input type="text" onclick="myFunction()" name="t1" id="pass"><br>
 		<button onclick="myFunction()">Next</button>
	</body>
</html>

2 Remove div section element after clicking on button using jQuery.
[Hint: Use #id selector]

HTML & JAVA Script FILe:
<!DOCTYPE html>
<html>
	<head>
  		<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
  		<script>
    			$(document).ready(function()
			{
      				$("#btn1").click(function()
				{
         				$('div').remove();
       				});	
    			});
  	</script>
	</head>

	<body>
 		<div >
  			This is div :(
 		</div>

		<button id="btn1">Next</button>
	</body>
</html>
Assignment4: AJAX
Set A

1 write AJAX program to read contact.dat file and print the contents of the file in a tabular format when the user Clicks on a print button. Contact.dat file should contain  Srno, name, residence number, mobile number, address. [Enter at least 3 record in a contact.dat file]

HTML File:
<html>
	<head>
		<style>
			span
			{
                		font-size: 25px;
			}
			table
			{
                		color: blueviolet; ;
			}
		</style>

		<script type="text/javascript">
                	function print()
                	{
                                var ob=false;
                                ob=new XMLHttpRequest();
             
                                ob.open("GET","A1.php");
                                ob.send();         
             
                                ob.onreadystatechange=function()
                                {
                                	if(ob.readyState==4 && ob.status==200)
                                        {
                                        	document.getElementById("i").innerHTML=ob.responseText;
                                        }
                                }
                	}           
		</script>
	</head>

	<body>
		<center>
			<h3>Display the contents of contact.dat file </h3>
			<br><input  type="button"  value="Print" onclick="print()" >
			<span id="i"></span>
		</center>
	</body>
</html>

PHP File:

<?php
	$fp = fopen('contact.dat',r);
	echo"<table border=1>";
	echo"<tr><th>Sr.No</th><th>Name</th><th>Residence Number</th><th>Mobile Number</th><th>Address</th></tr>";

	while($row = fscanf($fp,"%s %s %s %s %s"))
	{
		echo"<tr>";
		foreach($row as $r)
		{
			echo"<td>$r</td>";
		}
		echo"</tr>";
	}
	echo"</table>";
	fclose($fp);
?>



2  write AJAX program where the user is requested to write his or her name in a text box, and the server keeps sending back responses while the user is typing. if the user name is not entered then the message displayed will be, “stranger please tell me your name!”. if the name is Rohit, Virat, Dhoni, Ashwin or Harbhajan, the server response with hello Master <user name>!”.If the name is anything else,the message will be”<user name>,I don’t know you!”.


HTML File:
<html>
	<head>
		<script type="text/javascript">
			function print()
			{
   				var x=false;
   				x=new XMLHttpRequest();
   				t1 = document.getElementById("pass").value;
   				x.open("GET", "A2.php?t1="+t1,true);
   				x.send();
   				x.onreadystatechange=function()
   				{
      					if(x.readyState==4 && x.status==200)
      					{
           					document.getElementById("i").innerHTML=x.responseText;
      					}
   				}
			}  
		</script>
	</head>

	<body>
		Enter Name<input type ="text" name="t1" id="pass">
		<input type="button" value="submit" onclick="print()">
		<span id="i"></span>
	</body>
</html> 


PHP File:
<?php
 	$nm=$_GET['t1'];

 	$name=array("ROHIT","VIRAT","DHONI","ASHWIN","HARBHAJAN");
	if($nm==null)
	{
		echo "<br>Stranger, please tell me your name!";
	} 
	else if(in_array(strtoupper($nm), $name))
 	{
     		echo "<br>Hello Master " . $nm . "!";
  	}
 	else
 	{	
     		echo "<br>".$nm.",  I don't know you";
 	}
?>


Set B

1 create a teacher table as a follows(Tno,tname qualification, salary) write AJAX program to select a teacher's name and print the selected teachers details.


HTML File:
 <html>
<head>
<script type = "text/javascript">
function print()
{
   var x = false;
   x = new XMLHttpRequest();
   t1 = document.getElementById("pass").value;
   x.open("GET" , "ass4setb1.php?t1=" + t1,true);
   x.send();
   x.onreadystatechange = function()
   {
      if(x.readyState == 4 && x.status == 200)
      {
           document.getElementById("i").innerHTML = x.responseText;
      }
   }
}  
</script>
</head>
<body>
Enter Teacher Name <input type = "text" name = "t1" id = "pass">
<input type = "button" value = "submit" onclick = "print()">
<span id = "i"></span>
</body>
</html> 


2 write a AJAX program to print Order details by selecting a customer name. Create table customer and order as follows with 1:M cardinality CUSTOMER (cno, Cname, City) and ORDER (ono, odate, shipping address)


HTML File:
 <html>
	<script type= "text/javascript">
	function display()
	{
		ob= new XMLHttpRequest();
		var tnm=document.getElementById("tnm").value;
		ob.open("GET", "Assi4SetB2.php?tnm="+tnm, true);
		ob.send();
		ob.onreadystatechange= function()
		{
			if(ob.readyState==4 && ob.status==200)
			document.getElementById("i").innerHTML= ob.responseText;
		}
	}
	</script>
	<body>
		<h1>Display Order's details</h1>
		Enter Customer Name: <input type= text name= tnm id=tnm><br>
		<input type= submit value= Display onclick=display()>
		<span id=i></span>
	</body>
</html>
 

SET C:

1  Write Ajax program to fetch suggestions when is user is typing in a textbox. (eg like Google suggestions. Hint create array of suggestions and matching string will be displayed).


Html file :

<html>
<head>
<script type="text/javascript" >

         function m1(str)
         {
                     var ob=false;
                     ob=new XMLHttpRequest();
                                
                     ob.open("GET","slip_15.php?q="+str);
                     ob.send();        
        
                    
ob.onreadystatechange=function()
                     {
                                 if(ob.readyState==4 && ob.status==200)
                                 {
                                             document.getElementById("a").innerHTML=ob.responseText;
                                 }
                     }          
         }

</script>
</head>

<body>
<form>

Search<input type=text name=search size="20" onkeyup="m1(form.search.value)">

<input type=button value="submit" onclick="m1(form.search.value)">

</form>
suggestions :<span id="a"></span><br>

</body>
</html>

PHP file :

<?php
$a=array("pune","satara","nashik","sangli","mumbai","murud","akola","dound","dhule","ratnagiri","rajpur");

$q=$_GET['q'];

if(strlen($q)>0)
{       
         $match="";
         for($i=0;$i<count($a);$i++)
         {
                     if(strtolower($q)==strtolower(substr($a[$i],0,strlen($q))))
                     {
                                 if($match=="")
                                 $match=$a[$i];                         
                                             else $match=$match.",".$a[$i];
                     }          
         }
if($match=="")
echo "No Suggestios";
else echo $match;
}
?>
2 Write Ajax program to get book details from XML file when userselect a book name. Create XML file for storing details ofbook(title, author, year, price).


HTML File:

<html>
<body>
<script type="text/javascript">
function showHint(str)
{
    if(str == "")
    {
        document.getElementById("mydiv").innerHTML = "Error: select book";
        return;
    }
   if(window.XMLHttpRequest)
    {
        obj = new XMLHttpRequest();
    }
    else if(window.ActiveXObject)
    {
         obj = new ActiveXObject("Microsoft.XMLHTTP");
     }

    if(obj == null)
    {
       alert("Browser does not support HTTP request");
       return ;
     }
    var url = "ass4setc2.php";
    url = url +"?q=" + str;
   obj.open("GET" , url , true);
    obj.send(null);
    obj.onreadystatechange = function()
    {
          if(obj.readyState == 4 && obj.status == 200)
          {
              document.getElementById("mydiv").innerHTML = obj.responseText;
          }
    }
    
}
</script>
</head>
<body>
  <p><b>Book Name </b></p>
  <form>
  <select name = "bname" onchange = "showHint(this.value)">
  <option value ="">select book </option>
  <option value ="Java">Java</option>
  <option value ="C">C</option>
  </select>
  </form>
  <div id = "mydiv"><b>Book Info</b></div>
</body>
</html>


PHP File:

<?php 
$book1 = simplexml_load_file('book.xml');
$q = $_GET["q"];
 foreach($book1->book as $bnm)
 {
     if($bnm->bookname == $q)
     {
     echo "Book No =". $bnm->attributes()."<br>" ;
     echo "Book Name = $bnm->bookname "."<br>";
     echo "Author Name = $bnm->authorname "."<br>";
     echo "Price = $bnm->Price "."<br>";
     echo "Year = $bnm->year "."<br>";
    }
}

?>


XML File:


<?xml version='1.0' encoding='utf-8'?>
<bookinfo>
<Book code = "B1">
<bname>MOE </bname>
<Book_Title>Networking</Book_Title>
<Book_Author>400</Book_Author>
<Book_PubYear>2015</Book_PubYear>
<Book_Price>450</Book_Price>
</Book>
<Book code = "B2">
<bname>Java </bname>
<Book_Title>php </Book_Title>
<Book_Author>400</Book_Author>
<Book_PubYear>2015</Book_PubYear>
<Book_Price>450</Book_Price>
</Book>
</bookinfo>














