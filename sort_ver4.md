---
title: "快速排序与归并排序"
date: 2021-07-02
publishdate: 2021-07-02
lastmod: 2021-07-02
draft: false
tags: ["Algorithm"]
---

```Java
class Solution {
    //快排,时间复杂度，一般情况下O(nlogn),最差O(n^2),空间复杂度最好情况下O(logn),最坏O(n)
    public int[] sortArray(int[] nums) {
        quickSort(0,nums.length - 1,nums);
        return nums;
    }
    public void quickSort(int left, int right, int nums[]){
        if(left >= right){
            return;
        }
        int index = randomPartion(left,right,nums);
        quickSort(left, index - 1, nums);
        quickSort(index + 1, right, nums);
    }
    public int randomPartion(int left, int right, int nums[]){
        //定一个锚点，只要在left和right之间就行
         int i = new Random().nextInt(right - left + 1) + left;
         //把锚点放到最后
         swap(i,right,nums);
         return partion(left,right,nums);
    }
    public int partion(int left,int right,int[] nums){
        //比较的锚点
        int pivot = nums[right];
        //双指针，这个用来记录小元素的值
        int lowRange = left - 1;
        //从左到右依次和锚点比较
        for(int l = left; l <= right; l++){
            //比锚点小
            if(nums[l] < pivot){
                //lowRange进位
                //4,6,7,3,5   锚点是5, left range = -1 , l = 0;
                //4,6,7,3,5   锚点是5, left range = 0 , l = 3;
                lowRange++;
                //left range = 1 , l = 3; 4,3,6,7,5
                swap(l,lowRange,nums);
            }
        }
        //最后把锚点换到中间，也就是low range的下一个
        //4,3,6,7,5,range+1 = 2;
        //换完之后4,3,5,6,7
        swap(lowRange + 1,right,nums);
        return lowRange + 1;
    }
    public void swap(int left,int right,int[] nums){
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }



    //归并,时间复杂度稳定O(nlogn) 空间复杂度O(nlogn)
    public int[] sortArray(int[] nums) {
        temp = new int[nums.length];
        mergeSort(nums,0,nums.length - 1);
        return nums;
    }
    public void mergeSort(int[] nums,int left,int right){
        //最小的子数组,递归跳出
        if(left >= right){
            return;
        }
        //从两边开始归并，先得出中间index
        int middle = (right + left) / 2;
        //从中点开始，左右各一组递归
        mergeSort(nums,left,middle);
        mergeSort(nums,middle + 1,right);
        //将递归上来的两组排序好的数，插入排序合并
        //这里与合并两个有序链表差不多
        //不过不是链表，所以要把剩余的节点一个个进禁区
        int index = 0;
        int i = left;
        int j = middle + 1;
        for(; i <= middle && j <= right;){
            if(nums[i] >= nums[j]){
                temp[index++] = nums[j++]; 
            }else{
                temp[index++] = nums[i++];
            }
        }
        //补齐剩余的
        for(;i <= middle;){
            temp[index++] = nums[i++];
        }
        for(;j <= right;){
            temp[index++] = nums[j++];
        }
        //将插入排序好的temp数组放回原数组自己的位置中
        for(int x = 0; x < right - left + 1; x++){
            nums[x + left] = temp[x]; 
        }
    } 
}
```
