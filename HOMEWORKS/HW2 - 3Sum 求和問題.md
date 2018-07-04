HW2 - 3Sum 求和問題
===
## for loop
T(n) = n^3
```java=
public int T_sum(int[] A){
    int sum=0;
    for(int i=0; i<A.length; i++){
        for(int j=i+1; j<A.length; j++){
            for(int k=j+1; k<A.length; k++){
                if(A[i]+A[j]+A[k]==0) sum++;
            }
        }
    }
    return sum;
}
```

## Sort + Search
### Merge Sort + Binary Search
```java=
public int T_sum(int[] A){
    int sum=0;
    mergeSort(A);
    for(int i=0; i<A.length; i++){
        for(int j=i+1; j<A.length; j++){
            sum+=binarySearch(A,j+1,-A[i]-A[j]);
        }
    }
    return sum;
}
```
```java=
public void mergeSort(int[] A){
    int n = A.length;
    if(n<=1) return;
    
    int x=n/2, y=n-x;
    int[] left = new int[x];
    for(int i=0; i<x; i++) left[i]=A[i];
    int[] right = new int[y];
    for(int i=0; i<y; i++) right[i]=A[x+i];
    
    mergeSort(left);
    mergeSort(right);
    merge(A,left,right);
    return;
}
public void merge(int[] A, int[] left, int[] right){
    int i=0, j=0, k=0;
    int x=left.length, y=right.length;
    while(i<x && j<y){
        if(left[i]<right[j]){
            A[k] = left[i];
            i++;
        }else{
            A[k] = right[j];
            j++;
        }
        k++;
    }
    while(i<x){
        A[k] = left[i];
        i++;
        k++;
    }
    while(j<y){
        A[k] = right[j];
        j++;
        k++;
    }
    return;
}
```
```java=
public int binarySearch(int[] A, int low, int key){
    int up=A.length-1, mid;
    while(low<=up){
        mid=low+(up-low)/2;
        if(A[mid]==key) return 1;
        else if(A[mid]>key) up=mid-1;
        else low = mid+1;
    }
    return 0;
}
```
## Merge Sort + 2pointers
```java=
public int T_sum(int[] A){
    mergeSort(A);
    int result=0;
    for(int i=0; i<A.length-2 && A[i]<0; i++){
        int low=i+1, up=A.length-1, key=-A[i];
        while(low<up){
            if(A[low]+A[up]==key){
                result++;
                low++;
                up--;
            }else if(A[low]+A[up] > key) up--;
            else low++;
        }
    }
    return result;
}
```