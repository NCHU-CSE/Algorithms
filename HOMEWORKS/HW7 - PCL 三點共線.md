HW7 - PCL 三點共線
===
## Quick Sort
```java=
public boolean checkPCL(int[][] Arr){
	double[] a=new double[Arr.length*Arr.length/2];
	boolean check=false;
	int k=0;
	for(int i=0; i<Arr.length; i++){
		k=0;
		for(int j=i+1; j<Arr.length; j++){
			if((Arr[i][1]-Arr[j][1])==0){
				if(check==false) check=true;
				else return true;
			}else{
				a[k] = (double)(Arr[i][0]-Arr[j][0])/(Arr[i][1]-Arr[j][1]);
				k++;
			}
		}
		k--;
		qsort(a,0,k);
		for(int x=0; x<k; x++){
			if(a[x]==a[x+1]) return true;
		}
	}

	return false;
}
public void qsort(double[] A, int left, int right){
	if(left >= right){
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
## For Loop
```java=
public boolean checkPCL(int[][] Arr){
	for(int i=0; i<Arr.length; i++){
		for(int j=i+1; j<Arr.length; j++){
			for(int k=j+1; k<Arr.length; k++){
				if((Arr[i][0]-Arr[k][0])*(Arr[j][1]-Arr[k][1])==(Arr[j][0]-Arr[k][0])*(Arr[i][1]-Arr[k][1])) return true;
			}
		}
	}
	return false;
}
```