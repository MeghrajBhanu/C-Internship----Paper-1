
C++ Internship -- Paper 1
   
## Table of contents
*Question 1
*Question 2
  
## Question 1

Q1- Find the smallest and second smallest elements in an array.

Explanation- Write an efficient C program to find smallest and second smallest element in an array

Example:

Input: arr[] = {12, 13, 1, 10, 34, 1}
Output: The smallest element is 1 and
second Smallest element is 10
  

## Approach:
 
A naive approach for the above problem would be to Traverse the array and find the first smallest element,let it be x.Now we need to scan the array once again and find the minimum element which is greater than the first element.So basically,we traverse the array twice which will return the answer in O(n) time.
#h1 Time Complexity= O(n)+O(n)= 2(O(n)) (as we are traversing the array twice)
#h1 Ignoring the constant time complexity=O(n)
 
 A better solution would be to traverse the array once.Intialize two varaibles(first and second smallest elements ,say a and b)as MAX and loop through all the array elements and,
 Step 1:  if current element is smaller than a, then set a value to b and current element value to a. 
 Step 2:  Else if the current element is smaller than b and not equal to a set current element value to b.

 Time Complexity: O(n) (as traversing the array only once)
 base case: array size should be greater than or equal to two.
 Interesting case: Their may not be any second smallest element in case of duplicate elements(such as all the elemnts in the array may be same).
 Below is the implementation of above approach in C:
 
 ### Code:
 
```c

 #include<stdio.h>   //standard input output
 #include<limits.h>  //header file for INT_MAX
 int main(){
    int arr[6];  //array to store elements
    int n=6;
    int f=0,u=0;
    while(1){
        int i=scanf("%d",&f);
        if(i!=1)break;
        arr[u]=f;
        u++;
    }
    int length=sizeof(arr)/sizeof(arr[0]);  //length of array ...arr
    int a=INT_MAX,b=INT_MAX; //to strore first and second smallest elements
    if(length<2)printf("Invalid Input");
    for(int j=0;j<length;j++){
        if(arr[j]<a){  //refer step 1
            b=a;
            a=arr[j];
        }
        else if(arr[j]!=a && arr[j]<b){  //refer Step 2
            b=arr[j];
        }
    }
    if(b==INT_MAX){ //refer to Interesting case
        printf("The smallest element is %d",a);
        printf("Their is no second smallest element");
    }
    else{
        printf("The smallest element is %d and second Smallest element is %d",a,b);
        }
    return 0;
  }
  
```
       
## Question 2:

Q2-Find median in a stream of integers (running integers)

Explanation-
Given that integers are read from a data stream. Find median of elements read so for in efficient way. For simplicity assume there are no duplicates. For example, let us consider the stream 5, 15, 1, 3 …

After reading 1st element of stream - 5 -> median - 5
After reading 2nd element of stream - 5, 15 -> median - 10
After reading 3rd element of stream - 5, 15, 1 -> median - 5
After reading 4th element of stream - 5, 15, 1, 3 -> median - 4, so on...

            

## Approach:

Median: If number of elements are odd then middle element is median.
        If number of elements are even then average of middle numbers is median.
Using two heaps (max(lower half) and min heap(upper half))implemented with priority queue in STL library.
```
We try to balance the heap sizes while reading the element.If it is balanced then median is average of top elements of heaps.
If unbalanced median is top element of greater heap
```
<pre>
Intializing a variable mid=0 as initial value of median.

Read the element 

case 1:
If length(maxheap)==length(minheap) Then, If the element < mid then insert it to the max heap and update mid =maxheap.top(). If the element>mid then insert it to minheap and mid =minheap.top()

case 2:
If length(maxheap)<length(minheap) and the element > mid then pop minheap.top() insert it into  maxheap and insert the element to minheap else insert the element to the max heap.
Update mid = minheap.top()+maxheap.top() / 2.

case 3: 
If length(maxheap)>length(minheap) and element<mid then pop the maxheap.top() ,insert it into minheap and insert the element to max heap or else insert the element to minheap. 
Then update mid=minheap.top()+maxheap.top() / 2.
</pre>

Note: <b>Use double for storing elements as result median may be average of elemnts</b>

Below is implementation of above logic in c++:

## Code:

```c++
#include<bits/stdc++.h> 
using namespace std; 

int main() 
{ 
    double a;
    double arr[];
    int i=0;
    while(cin>>a){arr[i]=a; i++;}
    int n = sizeof(arr)/sizeof(arr[0]); 
    priority_queue<double,vector<double>,greater<double> > minheap; 
    priority_queue<double> maxheap; 
    double mid = arr[0]; 
    maxheap.push(arr[0]); 
    cout << mid << endl;   //after reading first element of the stream print it
    for (int i=1; i < n; i++) { 
        double current = arr[i]; 
        if (maxheap.size()==minheap.size()){ //refer case 1
            if (current<mid){
                maxheap.push(current); 
                mid = (double)maxheap.top(); 
            }
            else{ 
                minheap.push(current); 
                mid = (double)minheap.top(); 
            } 
        } 
        else if(maxheap.size()<minheap.size()){ //refer case 2
            if (current> mid) { 
                maxheap.push(minheap.top()); 
                minheap.pop(); 
                minheap.push(current); 
            } 
            else
                maxheap.push(x); 
            mid = (maxheap.top() + minheap.top())/2.0; 
        } 
        else if (maxheap.size() > minheap.size()){ 
            if (current< mid){
                minheap.push(maxheap.top()); 
                maxheap.pop(); 
                maxheap.push(current); 
            } 
            else minheap.push(current); 
            mid = (maxheap.top() + minheap.top())/2.0; 
        } 
        cout << mid << endl; 
      }
    return 0; 
}
```
     
