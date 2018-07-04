HW6 - Sorting Array
===
## Quick Sort
```java=
public int[] sorting(int[] A){
	qsort(A,0,A.length-1);
	return A;
}
```
```java=
public void qsort(int[] A, int left, int right){
	if(left+10 >= right){
		insert(A,left,right);
		return;
	}
	
	int pivot = A[(left+right)/2], tmp;
	int i = left-1, j = right+1;

	while(true){
		while(A[++i]<pivot);
		while(A[--j]>pivot);
		if(i>=j) break;

		tmp=A[i];
		A[i]=A[j];
		A[j]=tmp;
	}
	qsort(A,left,i-1);
	qsort(A,j+1,right);		
}
```
```java=
public void insert(int[] A, int left, int right){
	int x;
	for(int i=left+1; i<=right; i++){
		x=A[i];
		int j;
		for(j=i-1; j>-1 && x<A[j]; j--){
			A[j+1]=A[j];
		}
		A[j+1]=x;
	}
	return;
}
```