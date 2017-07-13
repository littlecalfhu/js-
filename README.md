# js-
.排序
一般都是给个数组然后排序，有的从小到大，有的从大到小。一定要看清楚。以下都是从小到大的排序算法。
冒泡法
var arr = [3,6,1,2,5];
var temp;
for(var i= 0;i<arr.length;i++){
for(var j=i+1;j<arr.length;j++){
if(arr[i] > arr[j]){
temp = arr[i];
arr[i] = arr[j];
arr[j] = temp;
}
}
}
console.log(arr);
快速排序法
function quicksort (arr){
 if(arr.length<=1){
 return arr;
 }
 var left = [];
 var right = [];
 var middle = arr[0];
 for(var i=1;i<arr.length;i++){
 if(arr[i]<middle){
 left.push(arr[i]);
 }else{
 right.push(arr[i]);
 }
 }
 return quicksort(left).concat([middle],quicksort(right));
}
注意：可以用快速就不要用冒泡。实在没记住才用冒泡。（因为快速排序设计到递归，面试官更多是想考察你递归算法）
2.数组去重
这题考察的是你会不会存储数组元素的出现次数来解决去重问题。当然解法也有很多，下面是其中一种解法。
Array.prototype.unique = function(){
 var res = [];
 var json = {};
 for(var i = 0; i < this.length; i++){
 if(!json[this[i]]){
 res.push(this[i]);
 json[this[i]] = 1;
 }
 }
 return res;
}
var arr = [112,112,34,'你好',112,112,34,'你好','str','str1'];
alert(arr.unique());
3.js的拷贝
这题涉及到的就是你能不能清楚的分辨深拷贝和浅拷贝。
var a = {name:'Tom'};  var b = a;  b.name = 'Peter'; 
请问a.name = ？
正确答案是Peter，如果你的答案是Tom的话，那么你要好好去看看js的深拷贝。
如果要被拷贝的是数组：
slice和concat都可以直接让数组进行深拷贝
arr.slice();
arr.concat();
下面是解法。当然肯定有比我写得更好的。
function deepCopy(source){
 var result = {};
 for(var i in source){
 if(typeof source[i] === "object"){
 result[i] = deepCopy(source[i]);
 }else{
 result[i] = source[i];
 }
 }
 return result;
}
4.获取字符串里出现子串的位置
function appear(str,str_target){
 var n = 0;
 var result = [];
 while(str.indexOf(str_target,n)!=-1 && n < str.length){
 result.push(str.indexOf(str_target,n));
 n = str.indexOf(str_target,n) + str_target.length;
 }
 return result;
}
var arr = appear('abascbascbabasbascbascascbab','ab');
console.log(arr);
5.不确定数量的数组遍历组合算法
好吧，解释下这题。这题在现实中确实会用到。尤其是做商城网站时，sku的算法真的经常会遇到。
这题的意思就是说。相当于说[1,2,3],[4,5]。。。。的不确定个数的数组进行遍历组合，组成[[1,4],[1,5],[2,4],[2,5],[3,4],[3,5]]这样。然后数组越多，组出来就肯定越多。
那怎么做的，我上网查了一些相关算法都没找到好的，然后我就自己写。可能还是会有点毛病，大家将就看。
有写的更好的欢迎评论教我一下。
function group(arr,re){
 if(arr.length <=0){
 return re;
 }
 if(!re){
 var arr = arr.slice();
 var re = arr.shift();
 return group(arr,re);
 }else{
 var now = arr.shift();
 var newre = [];
 for(var j=0;j<now.length;j++){
 for(var k=0;k<re.length;k++){
 var temp = [];
 if(re[k] instanceof Array){
  temp = re[k];
 }else{
  temp.push(re[k]);
 }
 newre.push(temp.concat(now[j]));
 }
 }
 return group(arr,newre);
 }
}
var arr = [['a','b','c'],['e','d','f'],['h','i'],['j','k','l','m']];
// var arr = [['a','b','c'],['e','d','f'],['h','i']];
// console.log(arr);
var result = group(arr);
console.log(result);
6.lazyMan(这道题考察了很多内容)
这道题自行百度吧。。只要百度lazyMan 面试题，应该是可以搜出来的
7.编写一个函数fn(Number n),将数字转为大写输出，如输入123，输出一百二十三。
好吧，这道题我是忘了我看的本站的哪位的文章了，觉得确实有点意思。
下面是他的代码。
function fn(n){
 if(!/^([1-9]\d*)/.test(n)){
  return '非法数据';
 }
 var unit = '千百十亿千百十万千百十个';
 if(n.length > unit.length){
  return '数据过长';
 }
 var newStr = '';
 var nlength = n.length;
 unit = unit.substr(unit.length - nlength);
 for(var i = 0; i < nlength; i++){
  newStr += '零一二三四五六七八九'.charAt(n[i]) + unit.charAt(i);
 }
 newStr = newStr.substr(0,newStr.length-1);
 newStr = newStr.replace(/零(千|百|十)/g,'零').replace(/(零)+/g,'零').replace(/零(亿|万)/g,'$1');
 return newStr;
}
console.log(fn('205402002103'));
8.如何将浮点数左边的数每三位添加逗号
如1200000.11转成12，000，000.11
result = num && num.toString().replace(/(\d)(?=(\d{3})+\.)/g,function($1,$2){
 return $2 + ',';
})
上面的解法是用正则，当然你也可以用别的方法。
