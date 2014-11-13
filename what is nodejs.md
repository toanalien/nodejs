# Nodejs là gì?

Theo như định nghĩa trên chính website của nó là:

> Node.js is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.

Nhưng như vậy là quá phức tạp. Hiểu một cách đơn giản là:

**Nodejs là một trình thông dịch của cho ngôn ngữ Javascript**. Sao lại nói như vậy?

1. Giả sử khi ta có ngôn ngữ PHP như:

	```php
	<?php
	    /*welcome.php*/
	    echo 'Hello world!';
	?>
	```
Khi execute `php welcome.php` thì nó sẽ thực thi cái file đó và output ra cái nội dung `Hello world!`

2. Với Nodejs ta có thể viết:
	
	```javascript
    /*welcome.js*/
    console.log('Hello world!');
	```
Khi execute `nodejs welcome.js` thì kết quả tương tự như với PHP.

> Điều này cho thấy, chúng ta có thể viết những cái script bằng ngôn ngữ Javascript để làm những chuyện tương tự như PHP, được thực thi thông quan Nodejs mà không cần thông qua trình duyệt. Và bài viết này sẽ cố gắng mô tả thông qua sự so sánh với PHP platform.

# So sánh Nodejs platform vs. PHP plaftorm (+ Apache)

## So sánh theo cơ chế hoạt động

Chúng ta thử tạo ra một hai ví dụ sau:

1. Với PHP (+Apache), mỗi khi truy xuất vào: [http://php.me](http://php.me) thì hiển thị ra dòng chữ `Hello World from PHP!`
2. Với Nodejs mỗi khi truy xuất vào [http://nodejs.me](http://nodejs.me) thì hiển thị ra dòng chữ `Hello World from Nodejs!`

Chúng ta sẽ có 2 đoạn code như sau:

1. Cho PHP

	```php
    <?php
    header('HTTP/1.0 200 OK');
    header('Content-Type: text/plain!');
    echo 'Hello World from PHP';
	```
2. Cho Nodejs (copy từ ví dụ official trên wesite của Nodejs)
	
	```javascript
    var http = require('http');
    http.createServer(function (req, res) {
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end('Hello World from Nodejs!');
    }).listen(1337, '127.0.0.1');
    console.log('Server running at http://127.0.0.1:1337/');
	```

### Thu hoạch số 1:

> Chúng ta có thể dùng Nodejs như PHP (+ Apache) để xử lý tương tự như là một web server.

## So sánh Javascript được viết ở phía Server vs. Client side

Ý này sẽ tập trung làm rõ vậy Javascript được viết ở Server side như ví dụ ở trên có gì khác biệt với Javascript được viết ở Client side?

1. Javacript được viết ở Client side thì bị hạn chế nhiều tính năng như:

        * Không thể đọc và ghi file v.v...
        * Được xứ lý bởi các trình thông dịch khác nhau của từng trình duyệt khác nhau như IE, Chrome, Firefox
        
2. Javascript được viết ở Client side thông dịch bằng Nodejs sẽ có nhiều tính năng hơn

        * Đọc và ghi file
        * Làm việc với hệ quản trị cơ sở dữ liệu như MySQL, MongoDB
        * Và cách tính năng khác có thể có như những gì chúng ta đã làm với PHP
        * Được xây dựng trên nền tảng V8 Engine - Cái nhân để thông dịch Javascript trên trình duyệt Chrome

### Thu hoạch số 2:

> Nói vậy thì chúng ta chả thấy nó so với PHP có gì hay. Mất thời gian học một ngôn ngữ khác mà chẳng có gì khác biệt. Trong khi PHP đã có tuổi, nhiều dự án thành công.

## Sự khác nhau cơ bản giữa PHP platform vs. Nodejs platform

Đúng là như vậy. Nếu chúng ta so sánh giữa iPhone5 vs với Nokia 1200 với tính năng thoại và sms thì rõ ràng điện thoại nào cũng như điện thoại nào. Tất nhiên, khi người ta phát triển một cái gì đó mới mẻ bao giờ cũng có ít nhất là triết lý, xa hơn nữa là lý do nhằm để giải quyết một hoặc nhiều vấn đề cụ thể nào đó.

Chúng ta sẽ đi qua một ví dụ khác:

Chúng ta viết một chương trình xây dựng bộ đếm đơn giản, cứ mỗi một request từ trình duyệt đén chúng ta sẽ tăng nó lên 1 đơn vị và hiện thị ở browser.

1. Cho PHP - Demo [http://php.me/counter.php](http://php.me/counter.php)
		
	```php
    <?php
    $view_number = @file_get_contents('view_number.txt');
    $view_number = $view_number + 1;
    @file_put_contents('view_number.txt', $view_number);
    echo 'Số lượt request: '. $view_number;
	```

2. Cho Nodejs - Demo [http://nodejs.me/counter.js](http://nodejs.me/counter.js)
	
	```javascript
    var view_number = 0;
    http.createServer(function (req, res) {
       view_number++;
       res.end(view_number.toString());
    }).listen(1337, '127.0.0.1');
	```

### Thu hoạch số 3:

> Tới đây chúng ta có thể thấy được rằng sự khác biệt đầu tiên là Nodejs chạy giống như một phần mềm `Desktop`. Nó không giống như PHP (+Apache) clear hết mọi thứ mỗi khi kết thúc một request. Biến view_number ở phía Nodejs vẫn được giữ lại và chỉ đơn giản là tăng lên sau mỗi lượt request mà thôi.

### Cải tiến cho PHP có thể work như Nodejs

Nói như vậy thì không same khi so sánh PHP (+Apache) vs. Nodejs. Bản thân Nodejs tự nó làm chức năng như một web server + handler. Mỗi khi có một request tới. Nó đơn giản là tạo ra một gọi cái callback mà chúng ta đã register để xứ lý. Do đó biến `view_numer` được chia sẽ/sử dụng lại như là biến toàn cục cho các function khác nhau. Nếu đứng ở view nhìn này, thì chúng ta cũng có thể dùng PHP để làm tương tự.

```php
<?php
error_reporting(E_ALL);
set_time_limit(0);
ob_implicit_flush();

$server         = create_socket();
$view_number    = 0;

do {
	$request = socket_accept($server);
	do {
		$respone   = ++$view_number.'';
		socket_write($request, $respone, strlen($respone));
		break;
	} while (true);
	socket_close($request);
} while (true);

socket_close($server);

function create_socket()
{
	$address    = '127.0.0.1';
	$port       = 10000;
	$sock       = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
	socket_bind($sock, $address, $port);
	socket_listen($sock, 5);
	return $sock;
}
```
	
### Thu hoạch số 4:

> Chúng ta có thể dùng PHP trong ngữ cảnh đơn giản này: counter số lượt request. Nhưng như vậy thì PHP và Nodejs khác biệc cơ bản là ở đâu?

## Cải tiến cho trường hợp phải restart lại Server
	
```javascript
var http        = require('http');
var fs          = require('fs');
var view_number = -1;

http.createServer(function (req, res) {
    /* Giải quyết vấn đề khởi động lần đầu tiên*/
    if( view_number === -1 ){
        console.log('Read this line only one time when the server is started');
        data = fs.readFileSync('view_number.txt');/*Hàm này đọc file cho đến khi nào được dữ liệu*/
        view_number = parseInt(data);
    }
    
    view_number++;
    res.end('Số lượt request: ' + view_number.toString());
    
    fs.writeFile("view_number.txt", view_number);/*Hàm này ghi file bất đồng bộ/
}).listen(1337, '127.0.0.1');
```

## Ứng dụng Nodejs để get FB data

Chúng ta sẽ bàn về vấn đề này, thông qua một ngữ cảnh cụ thể, với ví dụ sau đây:

> Request lên Facebook 200 basic info của user thông qua [graph.facebook.com/user_id](graph.facebook.com/user_id). Trong thời gian nhanh nhất.

### Phân tích sơ lược

Tạm thời không nghĩ tới các vấn đề kỹ thuật như Batch, FSQL để tiếp cận một ví dụ cho đơn giản để làm rõ vấn đề hiện tại của PHP là gì?

Như ai đã từng dùng xDebug để debug PHP, là khi chúng ta gọi một Graph API lên Facebook thông qua phương thức `Facebook::api(/<id_social_user>)` là cái hàm đó sẽ pending và đợi kết quả trả về.

> Thực sự vấn đề là bên trong PHP sẽ dùng `curl` để request lên Facebook và đợi kết quả trả về. Ở `curl` chúng ta cũng có option để nó không phải đợi và đi tới hàm tiếp theo. Nhưng rõ ràng điều này không thể app dụng cho FB request. Chúng ta chỉ làm điều này, chỉ khi nào chúng ta chỉ send một rquest lên server mà không cần nhận kết quả trả về.

Đến đây, tôi đã từng nghĩ rằng: **Vậy cũng đâu có sao, foreach 200 lần thôi.**

Nhưng vấn đề ở chỗ là có sự delay giữa mỗi một request, để đợi kết quả trả về. Giả sử thời gian delay do phải over network là 900ms mỗi một request. Thì tuần tự mỗi lần chúng ta sẽ tốn 9s cho 9 requests. Trong khi đó chúng ta nếu mở 10 connect cùng lúc. Thì có thể chỉ tốn khoản ~1s cho 9 request mà thôi. Có thẻ mở trình duyệt lên để kiếm chứng điều này. Trình duyệt sẽ mở một lần nhiều connect đến server để request file javascript, css, image v.v...

![No Thread](https://imanager-vlibs.googlecode.com/svn/branches/nodejs/trunk/nothread.png)

![Multi Thread](https://imanager-vlibs.googlecode.com/svn/branches/nodejs/trunk/multithread.png)

> Vậy là một lượng connect hợp lý đến server mà không cần bắt máy tính phải đợi là hợp lý hơn nhiều so với lần lượt từng connection một.

Vậy thì với PHP chúng ta chỉ cần gọi `php get_1_user_info.php user_id` 200 lần là được.

Nhưng mỗi lần làm như vậy PHP lại start một process, như vậy rất tốn kém tài nguyên. Và một máy tính thông thường, số lượng process có thể mở ra là có giới hạn. Chúng ta sẽ đi qua hai ví dụ tiếp theo để kiểm chứng điều này.

### Tiếp cận bằng ngôn ngữ PHP

#### Xử lý tuần tự 200 request

	
```php
<?php
error_reporting(0);
require 'facebook-php-sdk/src/facebook.php';

$facebook = new Facebook(array(
  'appId'  => '332332643458417',
  'secret' => '902ecc21e7f85e042c79997e9ac671a3',
));

/*Mot tap danh sach 200 FB user id */
$users = [
	'224982',
	//...
	'499614956',
	//...
	'499615103'
];

$start = microtime(true);
foreach($users as $user_id)
{
	print "-------------------------\n";
	$network_begin = microtime(true);
	$data = $facebook->api('/'.$user_id);
	print "Thoi gian over network la: ". (microtime(true) - $network_begin);
	print "\n";
	print_r($data);
}
$end = microtime(true);
echo "\n".'Tong thoi gian la: '. ($end - $start);
```

Gọi `php get_200_user_info.php >> log.txt` và `tail -f log.txt` để xem sự thực thi của nó.

> Demo này cho ta thấy việc foreach 200 lần để lấy user info là không khả thi. Vì thời gian over network cho mỗi connection là rất lâu.

#### Xử lý nhiều nhiều request cùng lúc.

Chúng ta sẽ phải tạo ra một file gọi là `get_1_user_info.php user_id` (tham số truyền vào là user id), và execute một lúc 200 lần như vậy cho 200 user id.
	
**Code của `get_1_user_info.php`**


```php
<?php
error_reporting(0);
require 'facebook-php-sdk/src/facebook.php';

$facebook = new Facebook(array(
  'appId'  => '332332643458417',
  'secret' => '902ecc21e7f85e042c79997e9ac671a3',
));

$user_id 	= $argv[1];
$index 		= $argv[2];

$start	= microtime(true);
$data 	= $facebook->api('/'.$user_id);
print $index.';'.(microtime(true) - $start);
print "\n";
```

Chúng ta cần một đoạn code để phân phối 200 user id cho `get_1_user_info.php`, file đó tạm gọi là: `master_get_user_info.php`

**Code của `master_get_user_ìnfo.php`**


```php
<?php
error_reporting(0);
/*Mot tap danh sach 200 FB user id */
$users = [
	'224982',
	//...
	'304332',
	//...
	'499615103'
];

$i = 1;
foreach($users as $user_id)
{
	exec("nohup php get_1_user_info.php $user_id $i >> log_200php.csv &");
	$i++;
}
```
	
Gọi `php master_get_user_info.php` sau đó thì `tail -f log_200php.csv` để xem chi tiết.

### Thu hoạch số 5

> Tới đây có thể chứng minh được như điều đã nói ban đầu là một lúc gọi nhiều request lên FB là tốt hơn. So với gọi tuần tự từng cái một.

### Tiếp cận bằng Nodejs

Chúng ta sẽ xem xét qua cách cũng cách làm trên nhưng implement bằng Nodejs thì sẽ như thế nào?

```javascript
var Facebook = require('facebook-node-sdk');

var facebook = new Facebook({ appId: '332332643458417', secret: '902ecc21e7f85e042c79997e9ac671a3' });
var users = [
'224982',
//...
'304332',
//...
'499615103'
];

var start = new Date().getTime();

for(var i in users)
{
	facebook.api('/'+users[i],
		function(err, data) {
			var end = new Date().getTime();
			if( data && data.id)
			{
				var duration = (end-start)/1000;
				console.log(users.indexOf(data.id)+';'+duration);
	  		}
		}
	);
}
```

### Sự khác biệt cơ bản

Nhưng chúng ta thấy đoạn code ở trên vì Nodejs được viết bằng ngôn ngữ Javascript, nên nó có support callback function, chúng ta có thể xử lý bất đồng bộ như AJAX mà chúng ta đã quen thuộc. Vậy liệu chúng ta có thể tiếp tục thay đổi code, để có thể viết PHP theo như cách ở trên không?
Câu trả lời là `KHÔNG`. Tại sao? Bởi vì PHP không support Theading dưới dạng built-in, ít nhất là tại thời điểm hiện tại. Do đó hãy nhìn lại ví dụ về đếm số lượng request. Câu hỏi đặt ra là, nếu chúng ta không phải làm cái việc đơn giản là tăng số giá trị của biến `view_number` lên một, mà là một xử lý gì đó tốn nhiều thời gian hơn thì điều gì xảy ra. Hàm `socket_accept` sẽ không được gọi. Và những connect khác sẽ không đến được.

![Nodejs vs. PHP CLI](https://imanager-vlibs.googlecode.com/svn/branches/nodejs/trunk/nodejs_vs_php.png)

### Thu hoạch số 6:

> Javascript/Nodejs support Threading dưới một cách native, do đó mà trong các vấn đề về xử lý bất đồng bộ, tiếp cận thông qua Nodejs là rất dễ dàng và đơn giản. Vì support multi-thread mà Nodejs dễ dang chia sẽ được tài nguyên vùng nhớ chung với nhau.

## Nodejs service ~ PHP push dữ liệu

Trong phần này, chúng ta sẽ cố gắng mô tả 2 điều chính:

1. Xây dựng một pool để chứa các request mà từ phía PHP Server push/send lên Nodejs Server.
2. Xây dựng một cơ chế để pop các message từ pool ra để xử lý.

	```javascript
    var http    = require('http');
    var url     = require('url');
    
    var pool        = [];
    
    var __main__    = function(){
        console.log('Length of Pool: ' + pool.length);
        setTimeout(__main__, 1000);
    };
    
    http.createServer(function (req, res) {
    var url_parts 	= url.parse(req.url, true);
        var query 		= url_parts.query;
        res.writeHead(200, {'Content-Type': 'text/plain'});
        
        if( query['id'] )
        {
            pool.push(query['id']);
            res.end('Recieved a request id:' + query['id']);
            return;
        }
        res.end('Pong');
    }).listen(1337, '127.0.0.1');
    
    __main__();
    ```

> Tại sao lại là khái niệm pool mà không phải stack:

1. Chúng ta sẽ không cố gắng mô tả giống như Stack: FIFO
2. Chúng ta implement cái pool ~ có nghĩa là một cái hồ chứa. Và nó có xử lý khi bị tràn.
3. Một cái pool + với các vấn đề về sự ưu tiên (priority) của message sẽ được implement một cách đầy đủ.

### Thu hoạch số 7:

> Chúng ta có thể dùng cái này để cung cấp giải pháp như là cập nhật lại thống kê cho user action mỗi khi một cái post change category của nó theo kiểu realtime. Bằng cách send lên server của Nodejs thông tin về cái page mà mình muốn cập nhật.

## Demo ~ Lấy likes info của một Post và insert vào MySQL

Sẽ là thiếu thuyết phục nếu như bài viết này không demo Nodejs với MySQL làm việc như thế nào? Chúng ta sẽ xem qua script bên dưới để xem Nodejs làm việc có khả thi không? Bằng cách lấy một lúc likes của 10 post và insert vào MySQL.

Lấy tất cả thông tin về likes của post: [http://www.facebook.com/10151600027848360](http://www.facebook.com/10151600027848360)

```javascript
var mysql      = require('mysql');
var Facebook = require('facebook-node-sdk');

var facebook = new Facebook({
	appId: '332332643458417',
	secret: '902ecc21e7f85e042c79997e9ac671a3'
});

//Docs: https://github.com/felixge/node-mysql
var connection = mysql.createConnection({
	host          : 'localhost',
	user          : 'root',
	password      : '',
	database      : 'master'
});

var i 				= 0,
	graph 			= '/10151600027848360/likes',
	id_social_post	= '10151600027848360',
	id_social_page 	= '290539813359',
	id_social_user	= null;

//Connect to facebook to get likes
facebook.api(graph,{
	limit: 100
},function(err, data){
	if( data['data'].length );
	{
		insertDataToDb(data['data']);
	}
	if( data['paging'] && data['paging']['next'] )
	{
		getNextPage(data['paging']['next']);		
	}
});

//Xu ly tuan tu cho next page
function getNextPage(url)
{
	facebook.api(url, function(err, data){
		if( data['data'].length );
		{
			insertDataToDb(data['data']);
		}	
		if( data['paging'] && data['paging']['next'] )
		{
			getNextPage(data['paging']['next'])
		}
	});
}

//Insert 100 rows to db each time
var total = 0;
function insertDataToDb(data)
{
	var strQuery 	= "INSERT INTO likes(id_social_user, id_social_post, id_social_page, created_time) VALUES ?";
	var arrInsert	= [];
	var created_time= parseInt(new Date().getTime()/1000);
	for(var i in data)
	{
		var _data = data[i];
		arrInsert.push([_data.id, id_social_post, id_social_page, created_time]);
	}
	total += data.length;
	console.log(total);
	connection.query(strQuery, [arrInsert], function(err) {
		if( err )
		{
			console.log('Have error');
			console.log(err);
		}
	});	
}
```
> Quan sát thấy chúng ta không lấy đủ dữ liệu của Like ~7000 vs. 65k

ST [https://github.com/tpphu/](@tpphu)