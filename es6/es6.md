# Mốt số ghi chép về ES6

## Arrow function

Để khai báo một closure function trong ES6 chúng ta sử dụng cú pháp:

``` javascript
(param1, param2,...,paramN) => {
  //content function
}
```

Trong đó: ```param1, param2,... paramN``` là các tham số chúng ta muốn truyền vào hàm (nếu có).

VD: 

``` javascript
var getName = () => {
    return "thaonv";
}
console.log(getName());
```

Nhưng do trong trường hợp này nội dung của function chỉ có có 1 dòng, nên chúng ta hoàn toàn có thể bỏ cặp dấu {} đi. Do đó VD trên sẽ thành như sau:

``` javascript
var getName = () => "thaonv";
console.log(getName());
```

Truyển vào tham số 

``` javascript
var getName = (name) => alert(name);
getName("thaonv");
```

Arrow function dùng với object 

``` javascript
var obj = {
    name: "thaonv",
    age: 22,
    getName: function (param) {
        console.log(param());
    },
    getAge: function (param) {
        console.log(param());
    },
    showAll : function () {
        //getName
        this.getName(() => {
            return "name: " + this.name;
        });
        //getAge
        this.getAge(() => {
            return "age: " + this.age;
        });
    }
}
obj.showAll();
```

## Rest Parameter

Tính năng này cho phép chúng ta có thể truyền vô số tham số vào hàm bằng cách thêm `...` vào trước tên tham số. Lúc này,tham số đó sẽ được coi như là một mảng tuần tự chứa các tham số truyền vào hàm.

``` javascript
function getSum(...c) {
    return Array.isArray(c);
}
alert(getSum());
//true
```

## Module

Đối với js trước đây thì tất cả các file mà có khởi tạo biến, hàm ,... thì các file load sau nó đều có thể sử dụng.

Nhưng giờ đây với ES6 thì chúng ta cũng đã có thể module hóa code javascript bằng cách sử dụng 2 keyword export và import với cú pháp như sau:

`export data;`

Trong đó: data là những gì bạn muốn xuất ra cho các module khác có thể sử dụng.

`import name from path;`

Trong đó:

- `name` là biến bạn muốn gán để nhận dữ liệu trả về từ module đó.
- `path` là đường dẫn chứa module bạn cần import.

VD:

``` javascript
/*file module.js*/
var getName = function () {
    return "thaonv";
}
var domain = "https://thaonv.xyz";
export {getName, domain}

/*file main.js*/
import {getName, domain} from "module.js";
//gọi hàm getName bên file module.js
getName();
//gọi biến domain
domain;
```

## Promise

Promise sinh ra để xử lý kết quả của một hành động cụ thể, kết quả của mỗi hành động sẽ là thành công hoặc thất bại và Promise sẽ giúp chúng ta giải quyết câu hỏi "Nếu thành công thì làm gì? Nếu thất bại thì làm gì?". Cả hai câu hỏi này ta gọi là một hành động gọi lại (callback action).

Khi một Promise được khởi tạo thì nó có một trong ba trạng thái sau:

- `Fulfilled` Hành động xử lý xông và thành công
- `Rejected` Hành động xử lý xong và thất bại
- `Pending` Hành động đang chờ xử lý hoặc bị từ chối

Tạo một promise 

`var promise = new Promise(callback);`

Trong đó callback là một function có hai tham số truyền vào như sau:

``` javascript
var promise = new Promise(function(resolve, reject){
     
});
```

Trong đó: 

- `resolve` là một hàm callback xử lý cho hành động thành công.
- `reject` là một hàm callback xử lý cho hành động thất bại.

**Thenable trong Promise**

Thenable không có gì to tác mà nó là một phương thức ghi nhận kết quả của trạng thái (thành công hoặc thất bại) mà ta khai báo ở Reject và Resolve. Nó có hai tham số truyền vào là 2 callback function. Tham số thứ nhất xử lý cho Resolve và tham số thứ 2 xử lý cho Reject.

``` javascript
var promise = new Promise(function(resolve, reject){
    resolve('Success');
    // OR
    reject('Error');
});
 
 
promise.then(
        function(success){
            // Success
        }, 
        function(error){
            // Error
        }
);
```

Vậy hai hàm callback trong `then` chỉ xảy ra một trong hai mà thôi, điều này tương ứng ở Promise sẽ khai báo một là Resolve và hai là Reject, nếu khai báo cả hai thì nó chỉ có tác dụng với khai báo đầu tiên.

**Catch trong Promise**

`then` có hai tham số callbacks đó là `success` và `error`. Tuy nhiên bạn cũng có thể sử dụng phương thức catch để bắt lỗi.

`promise.then().catch();`

``` javascript
var promise = new Promise(function(resolve, reject){
    reject('Error!');
});
 
 
promise
        .then(function(message){
            console.log(message);
        })
        .catch(function(message){
            console.log(message);
        });
```

nếu ta vừa truyền callback error và vừa sử dụng catch thì nó sẽ chạy hàm callback error và catche sẽ không chạy.

**Thenable liên tiếp**

Phương thức `then()` có nhiệm vụ tiếp nhận kết quả trả về của `promise` và nó cũng return về một promise nên bạn có thể dùng nhiều lần liên tiếp với nhau.

Nếu hành động của promise trả về là một Reject thì sẽ có hai trường hợp xảy ra như sau:

Trường hợp 1: Nếu trong phương thức then() nào đó có sử dụng callback function Reject thì các phương thức then() ở phía sau sẽ là một Fulfilled, nghĩa là nó sẽ chạy ở callback function Resolve

Trường hợp 2: Bạn sử dụng catch để bắt lỗi, lúc này chỉ có phương thức catch() là hoạt động.