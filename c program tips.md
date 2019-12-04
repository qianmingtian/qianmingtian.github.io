<!--
 * @Author: your name
 * @Date: 2019-11-06 09:25:34
 * @LastEditTime: 2019-11-06 09:29:42
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \qianmingtian.github.io\c program tips.md
 -->
+ ## 常量放在前面
if语句判断相等（==）时，把常量写前面:
```c
if($x == 1){
}
 
改成
 
if(1 == $x){

```
>常量放前面可以防止我们出现  如 x = 1 ;将判断句写成赋值句后难以察觉的错误,因为 常量是不能够作为左值的.

## 参考资料
[判断语句常量放前面](https://blog.csdn.net/cq_yj_818/article/details/47056891)

[为什么if语句判断相等(==)时，习惯把常量写前面](https://blog.csdn.net/cpongo3/article/details/89153078)