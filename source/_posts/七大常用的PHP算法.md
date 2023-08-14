title: 七大常用的PHP算法
date: 2016-01-26 12:24:36
tags: [php,算法]
---
`$arr = array(a,f,c,b,e,h,j,i,g);`
## 1、冒泡排序 
``` php
function bubble_sort($arr) {
    $n = count($arr);
    for($i = 0; $i < $n - 1; $i++){
        for($j = $i + 1; $j < $n; $j++) {
            if($arr[$j] < $arr[$i]) {
                $temp = $arr[$i];
                $arr[$i] = $arr[$j];
                $arr[$j] = $temp;
            }
        }
    }
    return $arr;
}
```
<!-- more -->
## 2、归并排序 
``` php
function merge(&$arr, $left, $mid, $right) {
  $i = $left;
  $j = $mid + 1;
  $k = 0;
  $temp = array();
  while ($i <= $mid && $j <= $right)
  {
    if ($arr[$i] <= $arr[$j])
      $temp[$k++] = $arr[$i++];
    else
      $temp[$k++] = $arr[$j++];
  }
  while ($i <= $mid)
    $temp[$k++] = $arr[$i++];
  while ($j <= $right)
    $temp[$k++] = $arr[$j++];
  for ($i = $left, $j = 0; $i <= $right; $i++, $j++)
    $arr[$i] = $temp[$j];
}
 
function merge_sort(&$arr, $left, $right)
{
  if ($left < $right)
  {
    $mid = floor(($left + $right) / 2);
    merge_sort($arr, $left, $mid);
    merge_sort($arr, $mid + 1, $right);
    merge($arr, $left, $mid, $right);
  }
}
```
## 3、二分查找-递归 
``` php
function bin_search($arr, $low, $high, $value) {
    if($low > $high)
        return false;
    else {
        $mid = floor(($low+$high)/2);
        if($value == $arr[$mid])
            return $mid;
        elseif($value < $arr[$mid])
            return bin_search($arr, $low, $mid-1, $value);
        else
            return bin_search($arr, $mid+1, $high, $value);
    }
}
```


## 4、二分查找-非递归 
``` php
function bin_search($arr, $low ,$high, $value) {
    while($low <= $high) {
        $mid = floor(($low + $high)/2);
        if($value == $arr[$mid])
            return $mid;
        elseif($value < $arr[$mid])
            $high = $mid - 1;
        else
            $low = $mid + 1;
    }
    return false;
}
```
## 5、快速排序 
``` php
function quick_sort($arr) {
    $n = count($arr);
    if($n <= 1)
        return $arr;
    $key = $arr[0];
    $left_arr = array();
    $right_arr = array();
    for($i = 1;$i < $n; $i++) {
        if($arr[$i] <= $key)
            $left_arr[] = $arr[$i];
        else
            $right_arr[] = $arr[$i];
    }
    $left_arr = quick_sort($left_arr);
    $right_arr = quick_sort($right_arr);
    return array_merge($left_arr, array($key), $right_arr);
}
```
## 6、选择排序 
``` php
function select_sort($arr) {
    $n = count($arr);
    for($i = 0; $i < $n; $i++) {
        $k = $i;
        for($j = $i + 1; $j < $n; $j++) {
           if($arr[$j] < $arr[$k])
               $k = $j;
        }
        if($k != $i) {
            $temp = $arr[$i];
            $arr[$i] = $arr[$k];
            $arr[$k] = $temp;
        }
    }
    return $arr;
}
```

## 7、插入排序 
``` php
function insert_sort($arr) {
    $n = count($arr);
    for($i = 1; $i < $n; $i++) {
        $tmp = $arr[$i];
        $j = $i-1;
        while($arr[$j] > $tmp) {
            $arr[$j+1] = $arr[$j];
            $arr[$j] = $tmp;
            $j--;
            if($j<0)
                break;
        }
    }
    return $arr;
}
```
