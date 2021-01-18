
C++ Internship -- Paper 1
   
   
   
Q1- Find the smallest and second smallest elements in an array.

Explanation- Write an efficient C program to find smallest and second smallest element in an array

Example:

Input: arr[] = {12, 13, 1, 10, 34, 1}
Output: The smallest element is 1 and
second Smallest element is 10
  

Explanation:
 
 A naive approach for the above problem would be to Traverse the array and find the first smallest element,let it be x.Now we need to scan the array once again and find the minimum element which is greater than the first element.So basically,we traverse the array twice which will return the answer in O(n) time.
 Time Complexity= O(n)+O(n)= 2(O(n)) (as we are traversing the array twice)
                  Ignoring the constant time complexity=O(n)
 
 A better solution would be to traverse the array once.Intialize two varaibles(first and second smallest elements ,say a and b)as MAX and loop through all the array elements and,
 Step 1:  if current element is smaller than a, then set a value to b and current element value to a. 
 Step 2:  Else if the current element is smaller than b and not equal to a set current element value to b.

 Time Complexity: O(n) (as traversing the array only once)
 base case: array size should be greater than or equal to two.
 Interesting case: Their may not be any second smallest element in case of duplicate elements(such as all the elemnts in the array may be same).
 Below is the implementation of above approach in C:
 <Code>
   
 #include<stdio.h>   //standard input output
 #include<limits.h>  //header file for INT_MAX
 int main(){
    int arr[6];  //array to store elements
    int n=6;
    int f=0,u=0;
    while(1)
    {
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
       
       
       
      
            
