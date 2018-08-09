### 1.插入排序
```php
<?php
function insert_sort($arr){
    $arr_length = count($arr);
    for($i=1;$i<$arr_length;$i++){
        $target = $arr[$i];
        for($j=$i-1;$j>=0;$j--){
            if($arr[$j]>$target){
                $arr[$j+1] = $arr[$j];
                $arr[$j] = $target;
            }else{
                break;
            }
        }
    }
    return $arr;
}

$arr=array(50,2,45,42,6,47,23,22,15,11,30,16,13,3);  
$sort_arr = insert_sort($arr);
echo "<pre>";
print_r($sort_arr);

?>
```
### 2.冒泡排序
```php
<?php
function m_sort($arr){
     $arr_length = count($arr);
     for($i=0;$i<$arr_length;$i++){
         for($j=$i+1;$j<$arr_length;$j++){
             if($arr[$i]>$arr[$j]){
                 $temp = $arr[$i];
                 $arr[$i] = $arr[$j];
                 $arr[$j] = $temp;
             }
         }
     }
     return $arr;
}
?>
```
