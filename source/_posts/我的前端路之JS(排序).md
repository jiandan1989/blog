title: JS排序
date: 2016-12-05 22:23:36
tags:
---

以前一直以为用了原生数组继承的sort函数就可以直接把数字内元素为数字的数组排序？原来我的理解一直是错误的。先上代码-->别人的

<!--more-->
```javascript
        var by = function(name){
            return function(o,p){
                var a,b ;
                if(typeof o === "object" && typeof p === "object" && o && p){
                    a = o[name];
                    b = p[name];
                    if(a === b){
                        return 0 ;
                    }
                    if(typeof a === typeof b ){
                        return a < b ? -1 : 1 ;
                    }
                    return typeof a < typeof b ? -1 : 1 ;
                }else{
                    throw("error");
                }
            }
        }


        //by2函数接受一个成员名字符串和一个可选的次要比较函数做为参数
        //并返回一个可以用来包含该成员的对象数组进行排序的比较函数
        //当o[age] 和 p[age] 相等时，次要比较函数被用来决出高下
        var by2 = function(name,minor){
            return function(o,p){
                var a,b;
                if(o && p && typeof o === 'object' && typeof p ==='object'){
                    a = o[name];
                    b = p[name];
                    if(a === b){
                        return typeof minor === 'function' ? minor(o,p):0;
                    }
                    if(typeof a === typeof b){
                        return a <b ? -1:1;
                                    }
                                    return typeof a < typeof b ? -1 : 1;
                }else{
                    thro("error");
                }
            }
        }

        const employees = [
            {name: "George", age: 32, retiredate: "March 12, 2014"},
            {name: "Edward", age: 17, retiredate: "June 2, 2023"},
            {name: "Christine", age: 58, retiredate: "December 20, 2036"},
            {name: "Sarah", age: 62, retiredate: "April 30, 2020"}
            ];

```

 这是一个用于操作数组内对象根据某个属性排序,可能会常用,所以放上边 不用往下翻了

 [string.prototype.localeCompare()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)


<!-- more -->

### 基本用法:

- #### 数组元素为字符串的排序

        var fruit = ['cherries', 'apples', 'bananas'];

        fruit.sort();//  => ['apples', 'bananas', 'cherries'];

无参数调用sort函数，默认是升序排列的，字母a,b,c排序结果正确

- #### 数组元素为数字的排序

        var array = [3,7,2,8,2,782,7,29,1,3,0,34];

        array.sort(); // => [0, 1, 2, 2, 29, 3, 3, 34, 7, 7, 782, 8]

是不是看起来时正常的,是正确的,其实这样的排序是错误的,什么原因呢？[点击查看MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
文档中明确说明了默认排序的规则是按照字符串的Unicode码位点(code point)排序

- #### 带参数的sort调用

先看一下将字符转为Unicode编码的函数

```javascript
        function array2unicode(arr){

            return arr.map(function(s){

                //先转为字符串

                s = String(s);

                //字符串拆分字符

                var charts = s.split('');

                //将每个字符转为unicode编码

                return charts.map(function(c){

                    return c.charCodeAt(0)

                });

            });
        };

        //举例

        var array = [12,3,13];

        array2unicode(array);//[49,50][51][49,51]

// 如果传入一个比较函数作为参数，如何实现默认的字符串排序效果呢？

        [12,3,13].sort(function(a,b){

            a = String(a);

            b = String(b);

            if(a < b) {

                return -1;

            }else if(a > b) {

                return 1;

            }else{

                return 0;

            }

        });

        // => [12,13,3];


上面是sort函数内部按照字符unicode编码排序，关键的关键在于返回0 -1 1 那么对于数字数组而言，我们更希望是按照数值进行排序，所以我们看到很多JS代码中对数字进行排序的自定函数是:


        var arr = [12,1,3,4];

        function sortBy(a,b){ //a,b表示相邻的两个数组元素

            return a - b ;

        }

        arr.sort(sortBy);//[1,3,4,12];
```
a - b 的值由三种情况

- 小于 0 时，a 排在 b 前面

- 大于 0 时， a 排在 b 后面

- 等于 0 时， a b 的相对位置不变

- #### 注意项

上面说到sort函数返回值可能有3个，那么下面的写法是错误的

        arr.sort(function(a,b){

            return a > b ;
        });

        //因为a > b 只能返回两种结果 true or false 相当于 1 or 0 然而并没有 -1

- Array.prototype.sort()的内部实现


           Quicksort is generally considered to be efficient and fast and so is used by V8 as the implementation for Array.prototype.sort() on arrays with more than 23 items. For less than 23 items,

           V8 uses insertion sort[2]. Merge sort is a competitor of quicksort as it is also efficient and fast but has the added benefit of being stable. This is why Mozilla and Safari use it for their implementation of Array.prototype.sort().



chrome 对 sort 做了特殊处理，对于长度小余 23 的数组使用的是 insert sort ，大于 23 使用的是 quicksort. quicksort 是不稳定的排序算法 , 因此 Mozilla 和 Safari 采 用了 merge sort 来实现. 由于所学有限，就不展开了


### 参考

- [https://www.nczonline.net/blog/2012/11/27/computer-science-in-javascript-quicksort/](https://www.nczonline.net/blog/2012/11/27/computer-science-in-javascript-quicksort/)

- [https://en.wikipedia.org/wiki/Sorting_algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm)

- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)


以上文章属摘编自[汤进伟](http://imweb.io/topic/565cf7253ad940357eb99881) 因为实在是找不到他的评论链接在什么地方,百度搜不到，所以就把他文章链接发上了，如果有看到的知道的可以告诉我。。。因为写博客真的是非常费劲的，以上纯属手动，除了数组内的值是复制之外。要尊重别人的劳动成果。


-----

### 下是摘自维基百科

- #### 稳定排序

    - [冒泡排序(Bubble Sort)](https://zh.wikipedia.org/wiki/%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F#.E5.8A.A9.E8.AE.B0.E7.A0.81)

            Array.prototype.bubble_sort = function() {
            	var i, j, temp;
            	for (i = 0; i < this.length - 1; i++)
            		for (j = 0; j < this.length - 1 - i; j++)
            			if (this[j] > this[j + 1]) {
            				temp = this[j];
            				this[j] = this[j + 1];
            				this[j + 1] = temp;
            			}
            	return this;
            };
            var num = [22, 34, 3, 32, 82, 55, 89, 50, 37, 5, 64, 35, 9, 70];
            num.bubble_sort();

    - [插入排序(insetion Sort)](https://zh.wikipedia.org/wiki/%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F)

             Array.prototype.insertion_sort = function() {
               	var i, j;
               	var temp;
               	for (i = 1; i < this.length; i++) {
               		temp = this[i];
               		j = i - 1;  // 如果将赋值放到下一行的for循环内, 会导致在第10行出现j未声明的错误
               		for (; j >= 0 && this[j] > temp; j--)
               			this[j + 1] = this[j];
               		this[j + 1] = temp;
              	}
              	return this;
              };

    - [鸡尾酒排序](https://zh.wikipedia.org/wiki/%E9%B8%A1%E5%B0%BE%E9%85%92%E6%8E%92%E5%BA%8F)

            Array.prototype.cocktail_sort = function() {
            	var i, left = 0, right = this.length - 1;
            	var temp;
            	while (left < right) {
            		for (i = left; i < right; i++)
            			if (this[i] > this[i + 1]) {
            				temp = this[i];
            				this[i] = this[i + 1];
            				this[i + 1] = temp;
            			}
            		right--;
            		for (i = right; i > left; i--)
            			if (this[i - 1] > this[i]) {
            				temp = this[i];
            				this[i] = this[i - 1];
            				this[i - 1] = temp;
            			}
            		left++;
            	}
            };
    - [桶排序(bucket sort)](https://en.wikipedia.org/wiki/Bucket_sort)

    - [归并排序(merge sort )](https://zh.wikipedia.org/wiki/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F)

             Array.prototype.merge_sort = function() {
             	var merge = function(left, right) {
             		var final = [];
             		while (left.length && right.length)
             			final.push(left[0] <= right[0] ? left.shift() : right.shift());
             		return final.concat(left.concat(right));
             	};
             	var len = this.length;
             	if (len < 2) return this;
             	var mid = len / 2;
             	return merge(this.slice(0, parseInt(mid)).merge_sort(), this.slice(parseInt(mid)).merge_sort());
             };

    -  [二叉搜索树](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%85%83%E6%90%9C%E5%B0%8B%E6%A8%B9)

    - [鸽巢排序](https://zh.wikipedia.org/wiki/%E9%B8%BD%E5%B7%A2%E6%8E%92%E5%BA%8F)

    - [基数排序](https://zh.wikipedia.org/wiki/%E5%9F%BA%E6%95%B0%E6%8E%92%E5%BA%8F)

    - [侏儒排序](https://en.wikipedia.org/wiki/Gnome_sort)


- #### 不稳定排序

    - [选择排序](https://zh.wikipedia.org/wiki/%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F)

            Array.prototype.selection_sort = function() {
                var i, j, min;
                var temp;
                for (i = 0; i < this.length - 1; i++) {
                    min = i;
                    for (j = i + 1; j < this.length; j++)
                        if (this[min] > this[j])
                            min = j;
                    temp = this[min];
                    this[min] = this[i];
                    this[i] = temp;
                }
            };

    - [希尔排序](https://zh.wikipedia.org/wiki/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F)

            Array.prototype.shell_sort = function() {
                var gap, i, j;
                var temp;
                for (gap = this.length >> 1; gap > 0; gap >>= 1)
                    for (i = gap; i < this.length; i++) {
                        temp = this[i];
                        for (j = i - gap; j >= 0 && this[j] > temp; j -= gap)
                            this[j + gap] = this[j];
                        this[j + gap] = temp;
                    }
            };

    - [梳排序](https://zh.wikipedia.org/wiki/%E6%A2%B3%E6%8E%92%E5%BA%8F)


            Array.prototype.comb_sort = function() {
                var shrink_factor = 0.8;
                var gap = this.length, swapped = 1, i;
                var temp;
                while (gap > 1 || swapped) {
                    if (gap > 1)
                        gap = Math.floor(gap * shrink_factor);
                    swapped = 0;
                    for (i = 0; gap + i < this.length; i++)
                        if (this[i] > this[i + gap]) {
                            temp = this[i];
                            this[i] = this[i + gap];
                            this[i + gap] = temp;
                            swapped = 1;
                        }
                }
                return this;
            };
    - [堆排序](https://zh.wikipedia.org/wiki/%E5%A0%86%E6%8E%92%E5%BA%8F)

              Array.prototype.heap_sort = function() {
                var arr = this.slice(0);
                function swap(i, j) {
                    var tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;
                }

                function max_heapify(start, end) {
                    //建立父節點指標和子節點指標
                    var dad = start;
                    var son = dad * 2 + 1;
                    if (son >= end)//若子節點指標超過範圍直接跳出函數
                        return;
                    if (son + 1 < end && arr[son] < arr[son + 1])//先比較兩個子節點大小，選擇最大的
                        son++;
                    if (arr[dad] <= arr[son]) {//如果父節點小於子節點時，交換父子內容再繼續子節點和孫節點比較
                        swap(dad, son);
                        max_heapify(son, end);
                    }
                }

                var len = arr.length;
                //初始化，i從最後一個父節點開始調整
                for (var i = Math.floor(len / 2) - 1; i >= 0; i--)
                    max_heapify(i, len);
                //先將第一個元素和已排好元素前一位做交換，再從新調整，直到排序完畢
                for (var i = len - 1; i > 0; i--) {
                    swap(0, i);
                    max_heapify(0, i);
                }

                return arr;
              };
              var a = [3, 5, 3, 0, 8, 6, 1, 5, 8, 6, 2, 4, 9, 4, 7, 0, 1, 8, 9, 7, 3, 1, 2, 5, 9, 7, 4, 0, 2, 6];
              console.log(a.heap_sort());

    - [快速排序](https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)
```javascript

            Array.prototype.quick_sort = function() {
            	var len = this.length;
            	if (len <= 1)
            		return this.slice(0);
            	var left = [];
            	var right = [];
            	var mid = [this[0]];
            	for (var i = 1; i < len; i++)
            		if (this[i] < mid[0])
            			left.push(this[i]);
            		else
            			right.push(this[i]);
            	return left.quick_sort().concat(mid.concat(right.quick_sort()));
            };
```
    - [耐心排序](https://zh.wikipedia.org/wiki/%E8%80%90%E5%BF%83%E6%8E%92%E5%BA%8F)

还有很多排序方法，但都不是经常用，所以就不再复制粘贴了

