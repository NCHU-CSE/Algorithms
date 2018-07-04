HW5 - Minimal of Rotating Array 旋轉陣列最小值
===
## For Loop
```java=
public int fold_min_1(int[] A){
	for(int i=1; i<A.length; i++){
		if(A[i]-A[i-1]<0) return A[i];
	}
	return A[0];
}
```
## Quick Select
```java=
public int fold_min(int[] A){
	int start=0, end=A.length-1;
	while(start<=end){
		if(start==end-1) return A[end];
		int mid=(start+end)/2;
		if(A[start]>A[mid]) end=mid;
		else if(A[end]<A[mid]) start=mid;
	}
	return A[0];
}
```