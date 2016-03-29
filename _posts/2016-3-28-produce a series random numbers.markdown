---
layout: post
title:  "随机产生一个不同大小数字的序列"
date:   2016-3-28 17:39:11 +0800
categories: rand
---
最近在做导师的项目过程中，需要用到一个不同大小的数字序列，从最开始，到现在一共用了两种方法，且相对来说，效率也越来越高，下面见源码：

第一种：
<pre>#define num 100
void main(){
    int a[num];
    int i;
    srand((unsigned)time(NULL));
    for(i=0;i<num;i++){
        a[i]=rand()%num;
        for(int j=0;j<i;j++){
           if (a[i]==a[j]){
           a[i]=rand()%num;
           j=-1;
           }
        }
    }
    for(i=0;i<num;i++)  cout<<a[i]<<"  ";
	
}
</pre>
第二种：

<pre>
	void main(){
        int a[10000],b[10000],b1,temp;
        for(int i=0;i<10000;i++){
          a[i]=i+1;
        }
        srand((unsigned)time(0));
        for(i=0;i<10000;i++){
          b1=rand()%(10000-i);
          b[i]=a[b1];
          for(int j=b1;j<(10000-i);j++)    a[j]=a[j+1];
        }
        for(i=0;i<10000;i++)    cout<<b[i]<<"\r";	
	
    }
</pre>
<h1>总结：</h1>
第一种方法属于暴力随机法，一个一个的产生，然后同之前产生好的序列进行对比，相同则重新产生，当规模较大时此方法效率低；第二种方法属于随机效率较高的随机法，首先产生一个序列，然后把该序列顺序打乱，规模大时，效率明显要高于第一种方法。