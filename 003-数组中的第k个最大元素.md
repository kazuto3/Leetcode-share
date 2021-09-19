### Leetcode215，数组中第k个最大元素

​		给定整数数组 `nums` 和整数 `k`，请返回数组中第 `**k**` 个最大的元素。

​		请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。



**思路：本题目考察的其实是对排序算法的应用，以下主要提供快排和堆排解决的思路和代码。**



方法一：快速排序，即每轮选取一个基准值，把比基准值小的放在左侧，比基准值大的放在它的右侧。采用递归的方式达到排序的效果。

![](https://img-blog.csdnimg.cn/a8bdc70df3fe4aafa13daa00dcdee0ac.jpg?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAdG9tY2F0MzMzMzMz,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



```java
package kazuto.sort;

import java.util.Arrays;

public class QuickSort {
    public static void main(String[] args) {
        int[] arr= {3,2,16,7,4,8,6,9,23,56};
        quickSort(arr,0,arr.length-1);
        System.out.println(Arrays.toString(arr));
    }

    private static void quickSort(int[] arr, int leftIndex, int rightIndex) {
        if(leftIndex>=rightIndex){
            return;
        }
        int left = leftIndex;
        int right = rightIndex;
        int key = arr[left];//基准值
        while(left<right){
            while(left<right&&arr[right]>=key){
                right--;
            }
            arr[left] = arr[right];

            while(left<right&&arr[left]<=key){
                left++;
            }
            arr[right] = arr[left];
        }
        arr[left] = key;//基准值归位
        quickSort(arr,leftIndex,left-1);
        quickSort(arr,right+1,rightIndex);
    }

}

```



方法二：堆排序，主要做两件事：构造大/小顶堆，交换堆顶元素与堆尾元素，调整堆结构

![](https://img-blog.csdnimg.cn/ba888f73a1034d75869c907f0044e258.jpg?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAdG9tY2F0MzMzMzMz,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



```java
package kazuto.sort;

import java.util.Arrays;

public class HeapSort {
    public static void main(String[] args) {
        int[] arr= {3,2,16,7,4,8,6,9,23,56};
        heapSort(arr);
        System.out.println(Arrays.toString(arr));
    }

    public static void heapSort(int[] arr){
        //构建大顶堆
        for(int i=arr.length/2-1;i>=0;i--){
            adjustHeap(arr,i,arr.length);
        }
        //调整堆结构+交换堆顶元素与末尾元素
        for(int j=arr.length-1;j>0;j--){
            swap(arr,0,j);
            adjustHeap(arr,0,j);
        }

    }

    private static void swap(int[] arr, int i, int i1) {
        int temp = arr[i];
        arr[i] = arr[i1];
        arr[i1] = temp;
    }

    private static void adjustHeap(int[] arr, int i, int length) {
        int temp = arr[i];//先取出当前元素
        for(int k=2*i+1;k<length;k=k*2+1){
            if(k+1<length&&arr[k]<arr[k+1]){
                k++;
            }
            if(arr[k]>temp){
                arr[i] = arr[k];
                i = k;
            }else{
                break;
            }
        }
        arr[i] = temp;
    }
}

```

