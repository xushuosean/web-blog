# 排序算法的实现之Javascript

话不多说，直接代码。

### 1.冒泡排序

> 1、依次比较相邻的两个数，如果前一个比后一个大，则交换两者的位置，否则位置不变
>
> 2、按照第一步的方法重复操作前length-1的数字，直到最后一个数

图形示例

![](https://github.com/xushuosean/web-blog/blob/master/images/59b4fd9b000133a904950230.gif)

代码如下：

```javascript
function bubbleSort(nums) {
			var key = 0;
			for (var i = 0; i < nums.length - 1; i++) {
				for (var j = i + 1; j < nums.length; j++) {
					if (nums[i] > nums[j]) {
						key = nums[i];
						nums[i] = nums[j];
						nums[j] = key;
					}
				}
			}
			return nums;
		}
```

### 2.选择排序

> 1、依次找出最小的数，和前面的数交换位置

图形示例

![](https://github.com/xushuosean/web-blog/blob/master/images/59b500fb00011c7e06950221.gif)

代码如下：

```javascript
function select(nums){
			var item =0;
			for(var i = 0;i<nums.length-1;i++){
				var min = i;								//把最小索引给min
				for(var j = i+1;j<nums.length;j++){
					if(nums[min] > nums[j]) {				//对比,如果最小索引的vlaue大于其他value,则将该索引给min
						min = j								
					}
				}				
				item = nums[min];							//最小索引给他
				nums[min] = nums[i];
				nums[i] = item;
			}
			return nums;
		}
```

### 3、快速排序

> 1、找到中间的那个数作为基准，遍历数组，把小于基准的数放在left数组中，大于基准的数放在right数组中
>
> 2、再按同样的方法，对这两个数组进行排序
>
> 3、递归

图形示例：

![](https://github.com/xushuosean/web-blog/blob/master/images/59b501710001c41107450230.gif)

代码如下：

```javascript
var quickSort = function(nums) {
			if (nums.length <= 1) return nums;
			var pivotIndex = Math.floor(nums.length / 2);
			var pivot = nums.splice(pivotIndex, 1)[0]; //splice返回的是一个数组,所以用[0]取出来
			var left = [];
			var right = [];
			for (var i = 0; i < nums.length; i++) {
				if (nums[i] < pivot) {
					left.push(nums[i]);
				} else {
					right.push(nums[i]);
				}
			}

			return quickSort(left).concat(pivot, quickSort(right)); //使用递归完成快排
		}
```

### 4、插入排序

> 1、把一个数组分为【已排序】和【未排序】两部分，设定第一个数【已排序】，其余为【未排序】
>
> 2、从【未排序】中抽出第一个数，依次向前和【已排序】部分比较，如果比抽出的数大，则继续向前比较，否则插入后一个点

图形示例：

![](https://github.com/xushuosean/web-blog/blob/master/images/59b50130000191b706770214.gif)

代码如下：

```javascript
function insertionSort(nums) {
			var i,j,value;
			var len  = nums.length;
			for(i = 0;i<len;i++){
				value = nums[i];
				for(j = i-1;j>=0&&nums[j]>value;j--){
					nums[j+1] = nums[j];						//向后移一位
				}
				nums[j+1] = value;
			}
			return nums
		}

```

