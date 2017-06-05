# 排序算法

标签（空格分隔）： 算法

---

[TOC]

gif展示算法，并且配有java实现代码

##冒泡排序

![冒泡排序排序过程][1]
  
```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    bub(ints);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 冒泡排序
 */
public static void bub(int[] bubSrc) {
    int temp;
    for (int i = 0; i < bubSrc.length - 1; i++) {
        for (int j = 0; j < bubSrc.length - i - 1; j++) {
            if (bubSrc[j + 1] < bubSrc[j]) {
                temp = bubSrc[j];
                bubSrc[j] = bubSrc[j + 1];
                bubSrc[j + 1] = temp;
            }
        }
    }
}
```

##选择排序

![选择排序排序过程][2]

```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    sel(ints);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 选择排序
 */
public static void sel(int[] selSrc) {
    int n = selSrc.length;
    for (int i = 0; i < n; i++) {
        int k = i;
        for (int j = i + 1; j < n; j++) {
            if (selSrc[j] < selSrc[k]) {
                k = j;
            }
        }
        if (k > i) {
            int tmp = selSrc[i];
            selSrc[i] = selSrc[k];
            selSrc[k] = tmp;
        }
    }
}
```

##插入排序

![插入排序排序过程][3]

```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    inst(ints);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 选择排序
 */
public static void inst(int[] insSrc) {
    for (int i = 1; i < insSrc.length; i++) {
        if (insSrc[i - 1] > insSrc[i]) {
            int temp = insSrc[i];
            int j = i;
            while (j > 0 && insSrc[j - 1] > temp) {
                insSrc[j] = insSrc[j - 1];
                j--;
            }
            insSrc[j] = temp;
        }
    }
}
```

##归并排序

![归并排序排序过程][4]

```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    mer(ints);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 归并排序
 */
public static int[] mer(int[] nums, int low, int high) {
    int mid = (low + high) / 2;
    if (low < high) {
        // 左边
        mer(nums, low, mid);
        // 右边
        mer(nums, mid + 1, high);
        // 左右归并
        merge(nums, low, mid, high);
    }
    return nums;
}

public static void merge(int[] nums, int low, int mid, int high) {
    int[] temp = new int[high - low + 1];
    int i = low;// 左指针
    int j = mid + 1;// 右指针
    int k = 0;

    // 把较小的数先移到新数组中
    while (i <= mid && j <= high) {
        if (nums[i] < nums[j]) {
            temp[k++] = nums[i++];
        } else {
            temp[k++] = nums[j++];
        }
    }

    // 把左边剩余的数移入数组
    while (i <= mid) {
        temp[k++] = nums[i++];
    }
    
    // 把右边边剩余的数移入数组
    while (j <= high) {
        temp[k++] = nums[j++];
    }

    // 把新数组中的数覆盖nums数组
    for (int k2 = 0; k2 < temp.length; k2++) {
        nums[k2 + low] = temp[k2];
    }
}
```

##快速排序

![快速排序排序过程][5]

```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    mer(ints);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 快速排序
 */
public static void qui(int[] a,int low,int high){
    int start = low;
    int end = high;
    int key = a[low];
    while(end>start){
        //从后往前比较
        while(end>start&&a[end]>=key)//如果没有比关键值小的，比较下一个，直到有比关键值小的交换位  置，然后又从前往后比较
            end--;
        if(a[end]<=key){
            int temp = a[end];
            a[end] = a[start];
            a[start] = temp;
        }
        //从前往后比较
        while(end>start&&a[start]<=key)//如果没有比关键值大的，比较下一个，直到有比关键值大的交换位置
            start++;
            if(a[start]>=key){
                int temp = a[start];
                a[start] = a[end];
                a[end] = temp;
            }
            //此时第一次循环比较结束，关键值的位置已经确定了。左边的值都比关键值小，右边的值都比关键值大，但是两边的顺序还有可能是不一样的，进行下面的递归调用
        }
    //递归
    if(start>low) qui(a,low,start-1);//左边序列。第一个索引位置到关键值索引-1
    if(end<high) qui(a,end+1,high);//右边序列。从关键值索引+1到最后一个
}
```

##计数排序

![计数排序排序过程][6]

```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    cou(ints，12);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 计数排序
 */
public static void cou(int[] array, int range) throws Exception {
    if (range <= 0) {
        throw new Exception("range can't be negative or zero.");
    }

    if (array.length <= 1) {
        return;
    }

    int[] countArray = new int[range + 1];
    for (int i = 0; i < array.length; i++) {
        int value = array[i];
        if (value < 0 || value > range) {
            throw new Exception("array element overflow range.");
        }
        countArray[value] += 1;
    }

    for (int i = 1; i < countArray.length; i++) {
        countArray[i] += countArray[i - 1];
    }

    int[] temp = new int[array.length];
    for (int i = array.length - 1; i >= 0; i--) {
        int value = array[i];
        int position = countArray[value] - 1;

        temp[position] = value;
        countArray[value] -= 1;
    }

    for (int i = 0; i < array.length; i++) {
        array[i] = temp[i];
    }
}
```

##基数排序

![基数排序排序过程][7]

```java
public static void main(String[] args) {
    int[] ints = new int[]{12, 3, 8, 6, 2, 4, 1, 5, 7, 9, 10};
    cou(ints，12);
    printInts(ints);
}

public static void printInts(int[] ints) {
    for (int i : ints) {
        System.out.print(i + ",");
    }
}

/**
 * 基数排序
 */
public static void radixSort(int[] data, int radix, int d) {
    // 缓存数组
    int[] tmp = new int[data.length];
    // buckets用于记录待排序元素的信息
    // buckets数组定义了max-min个桶
    int[] buckets = new int[radix];

    for (int i = 0, rate = 1; i < d; i++) {

        // 重置count数组，开始统计下一个关键字
        Arrays.fill(buckets, 0);
        // 将data中的元素完全复制到tmp数组中
        System.arraycopy(data, 0, tmp, 0, data.length);

        // 计算每个待排序数据的子关键字
        for (int j = 0; j < data.length; j++) {
            int subKey = (tmp[j] / rate) % radix;
            buckets[subKey]++;
        }

        for (int j = 1; j < radix; j++) {
            buckets[j] = buckets[j] + buckets[j - 1];
        }

        // 按子关键字对指定的数据进行排序
        for (int m = data.length - 1; m >= 0; m--) {
            int subKey = (tmp[m] / rate) % radix;
            data[--buckets[subKey]] = tmp[m];
        }
        rate *= radix;
    }
}
```

  [1]: http://wx1.sinaimg.cn/large/804bccdbly1fga2lvgi5mg20i4072wru.gif
  [2]: http://wx4.sinaimg.cn/large/804bccdbly1fga37hgvqfg20i4072nfp.gif
  [3]: http://wx4.sinaimg.cn/large/804bccdbly1fga3sahlhkg20i40eqgzv.gif
  [4]: http://wx4.sinaimg.cn/large/804bccdbly1fga41mmra7g20i40eq14m.gif
  [5]: http://wx2.sinaimg.cn/large/804bccdbly1fga47jvk3ig20i4072k6w.gif
  [6]: http://wx2.sinaimg.cn/large/804bccdbly1fga4vwt4olg20i40fuaf3.gif
  [7]: http://wx1.sinaimg.cn/large/804bccdbly1fga561z4cpg20s30gun2g.gif
