HW3 - ThreeSumMax 三和最大值
===
## Merge Sort
T(n) = nlog(n)
```java=
public int T_Max(int[] A){
	mergeSort(A);
	return A[A.length-1]+A[A.length-2]+A[A.length-3];
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
## Find the top three values ​​separately
T(n) = 3n
```java=
public int T_Max(int[] A){
	int m1=0, max1=A[0];
	for(int i=1; i<A.length; i++){
		if(A[i]>max1){
			m1=i;
			max1=A[i];
		}
	}
	int m2=0, max2=-2147483648;
	for(int i=0; i<A.length-1; i++){
		if(i==m1) continue;
		if(A[i]>max2){
			m2=i;
			max2=A[i];
		}
	}
	int m3=0, max3=-2147483648;
	for(int i=0; i<A.length-1; i++){
		if(i==m1 || i==m2) continue;
		if(A[i]>max3){
			m3=i;
			max3=A[i];
		}
	}
	return max1+max2+max3;
}
```
## Variant of Divide and Conquer
### Update from thrid place
```java=
public int T_Max(int[] A){
	int first=-2147483648, second=-2147483648, third=-2147483648;
	for(int i=0; i<A.length; i++){
		if(A[i]>third){
			if(A[i]>second){
				if(A[i]>first){
					third=second;
					second=first;
					first=A[i];
				}else{
					third=second;
					second=A[i];
				}
			}else{
				third=A[i];
			}
		}
	}
	return first+second+third;
}
```
### Update from first place
```java=
public int T_Max(int[] A){
	int first=-2147483648, second=-2147483648, third=-2147483648;
	for(int i=0; i<A.length; i++){
		if(A[i]>first){
			third=second;
			second=first;
			first=A[i];
		}else if(A[i]>second){
			third=second;
			second=A[i];
		}else if(A[i]>third){
			third=A[i];
		}
	}
	return first+second+third;
}
```