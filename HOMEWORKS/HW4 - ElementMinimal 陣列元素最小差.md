HW4 - ElementMinimal 陣列元素最小差
===
find the minimum difference between any two elements
## For Loop
```java=
public double Ele_Min(double[] A){
	double min=2147483647;
	for(int i=0; i<A.length; i++){
		for(int j=i+1; j<A.length; j++){
			if(A[i]-A[j]>0){
				if(A[i]-A[j]<min) min=A[i]-A[j];
			}else{
				if(A[j]-A[i]<min) min=A[j]-A[i];
			}
		}
	}
	return min;
}
```
## Merge Sort
```
public double Ele_Min_1(double[] A){
	mergeSort(A);
	double min=2147483647;
	for(int i=1; i<A.length; i++){
		if(A[i]-A[i-1]<min) min=A[i]-A[i-1];
	}
	return min;
}
```
```java=
public void mergeSort(double[] A){
	int n = A.length;
	if(n<=1) return;
	int x=n/2, y=n-x;
	double[] left = new double[x];
	for(int i=0; i<x; i++) left[i]=A[i];
	double[] right = new double[y];
	for(int i=0; i<y; i++) right[i]=A[x+i];
	mergeSort(left);
	mergeSort(right);
	merge(A,left,right);
	return;
}

public void merge(double[] A, double[] left, double[] right){
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
## Quick Sort
```java=
public double Ele_Min(double[] A){
	qsort(A,0,A.length-1);
	double min=A[1]-A[0];
	for(int i=2; i<A.length; i++){
		if(A[i]-A[i-1]<min) min=A[i]-A[i-1];
	}
	return min;
}
```
```java=
public void qsort(double[] A, int left, int right){
	if(left+10 >= right){
		insert(A,left,right);
		return;
	}
	
	double pivot = A[(left+right)/2], tmp;
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
public void insert(double[] A, int left, int right){
	double x;
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