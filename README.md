# js-
.排序<br/>
一般都是给个数组然后排序，有的从小到大，有的从大到小。一定要看清楚。以下都是从小到大的排序算法。<br/>
冒泡法<br/>
var arr = [3,6,1,2,5];<br/>
var temp;<br/>
for(var i= 0;i<arr.length;i++){<br/>
 for(var j=i+1;j<arr.length;j++){<br/>
    if(arr[i] > arr[j]){<br/>
       temp = arr[i];<br/>
       arr[i] = arr[j];<br/>
       arr[j] = temp;<br/>
    }<br/>
  }<br/>
}<br/>
console.log(arr);<br/>
快速排序法<br/>
function quicksort (arr){<br/>
 if(arr.length<=1){<br/>
 return arr;<br/>
 }
 var left = [];<br/>
 var right = [];<br/>
 var middle = arr[0];<br/>
 for(var i=1;i<arr.length;i++){<br/>
 if(arr[i]<middle){<br/>
 left.push(arr[i]);<br/>
 }else{<br/>
 right.push(arr[i]);<br/>
 }<br/>
 }<br/>
 return quicksort(left).concat([middle],quicksort(right));<br/>
}<br/>
注意：可以用快速就不要用冒泡。实在没记住才用冒泡。（因为快速排序设计到递归，面试官更多是想考察你递归算法）<br/>
2.数组去重<br/>
这题考察的是你会不会存储数组元素的出现次数来解决去重问题。当然解法也有很多，下面是其中一种解法。<br/>
Array.prototype.unique = function(){<br/>
 var res = [];<br/>
 var json = {};<br/>
 for(var i = 0; i < this.length; i++){<br/>
 if(!json[this[i]]){<br/>
 res.push(this[i]);<br/>
 json[this[i]] = 1;<br/>
 }<br/>
 }<br/>
 return res;<br/>
}<br/>
var arr = [112,112,34,'你好',112,112,34,'你好','str','str1'];<br/>
alert(arr.unique());<br/>
3.js的拷贝<br/>
这题涉及到的就是你能不能清楚的分辨深拷贝和浅拷贝。<br/>
var a = {name:'Tom'};  var b = a;  b.name = 'Peter'; <br/>
请问a.name = ？<br/>
正确答案是Peter，如果你的答案是Tom的话，那么你要好好去看看js的深拷贝。<br/>
如果要被拷贝的是数组：<br/>
slice和concat都可以直接让数组进行深拷贝<br/>
arr.slice();<br/>
arr.concat();<br/>
下面是解法。当然肯定有比我写得更好的。<br/>
function deepCopy(source){<br/>
 var result = {};<br/>
 for(var i in source){<br/>
 if(typeof source[i] === "object"){<br/>
 result[i] = deepCopy(source[i]);<br/>
 }else{<br/>
 result[i] = source[i];<br/>
 }<br/>
 }<br/>
 return result;<br/>
}<br/>
4.获取字符串里出现子串的位置<br/>
function appear(str,str_target){<br/>
 var n = 0;<br/>
 var result = [];<br/>
 while(str.indexOf(str_target,n)!=-1 && n < str.length){<br/>
 result.push(str.indexOf(str_target,n));<br/>
 n = str.indexOf(str_target,n) + str_target.length;<br/>
 }<br/>
 return result;<br/>
}<br/>
var arr = appear('abascbascbabasbascb<br/>ascascbab','ab');<br/>
console.log(arr);<br/>
5.不确定数量的数组遍历组合算法<br/>
好吧，解释下这题。这题在现实中确实会用到。尤其是做商城网站时，sku的算法真的经常会遇到。<br/>
这题的意思就是说。相当于说[1,2,3],[4,5]。。。。的不确定个数的数组进行遍历组合，组成[[1,4],[1,5],[2,4],[2,5],[3,4],[3,5]]这样。然后数组越多，组出来就肯定越多。
那怎么做的，我上网查了一些相关算法都没找到好的，然后我就自己写。可能还是会有点毛病，大家将就看。<br/>
有写的更好的欢迎评论教我一下。<br/>
function group(arr,re){<br/>
 if(arr.length <=0){<br/>
 return re;<br/>
 }<br/>
 if(!re){<br/>
 var arr = arr.slice();<br/>
 var re = arr.shift();<br/>
 return group(arr,re);<br/>
 }else{<br/>
 var now = arr.shift();<br/>
 var newre = [];<br/>
 for(var j=0;j<now.length;j++){<br/>
 for(var k=0;k<re.length;k++){<br/>
 var temp = [];<br/>
 if(re[k] instanceof Array){<br/>
  temp = re[k];<br/>
 }else{<br/>
  temp.push(re[k]);<br/>
 }<br/>
 newre.push(temp.concat(now[j]));<br/>
 }<br/>
 }<br/>
 return group(arr,newre);<br/>
 }<br/>
}<br/>
var arr = [['a','b','c'],['e','d','f'],['h','i'],['j','k','l','m']];<br/>
// var arr = [['a','b','c'],['e','d','f'],['h','i']];<br/>
// console.log(arr);<br/>
var result = group(arr);<br/>
console.log(result);<br/>
6.lazyMan(这道题考察了很多内容)<br/>
这道题自行百度吧。。只要百度lazyMan 面试题，应该是可以搜出来的<br/>
7.编写一个函数fn(Number n),将数字转为大写输出，如输入123，输出一百二十三。<br/>
好吧，这道题我是忘了我看的本站的哪位的文章了，觉得确实有点意思。<br/>
下面是他的代码。<br/>
function fn(n){<br/>
 if(!/^([1-9]\d*)/.test(n)){<br/>
  return '非法数据';<br/>
 }<br/>
 var unit = '千百十亿千百十万千百十个';<br/>
 if(n.length > unit.length){<br/>
  return '数据过长';<br/>
 }<br/>
 var newStr = '';<br/>
 var nlength = n.length;<br/>
 unit = unit.substr(unit.length - nlength);<br/>
 for(var i = 0; i < nlength; i++){<br/>
  newStr += '零一二三四五六七八九'.charAt(n[i]) + unit.charAt(i);<br/>
 }<br/>
 newStr = newStr.substr(0,newStr.length-1);<br/>
 newStr = newStr.replace(/零(千|百|十)/g,'零').replace(/(零)+/g,'零').replace(/零(亿|万)/g,'$1');<br/>
 return newStr;<br/>
}<br/>
console.log(fn('205402002103'));<br/>
8.如何将浮点数左边的数每三位添加逗号<br/>
如1200000.11转成12，000，000.11<br/>
result = num && num.toString().replace(/(\d)(?=(\d{3})+\.)/g,function($1,$2){<br/>
 return $2 + ',';<br/>
})<br/>
上面的解法是用正则，当然你也可以用别的方法。<br/>
