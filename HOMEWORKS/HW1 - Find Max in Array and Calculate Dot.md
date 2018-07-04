HW1 - Find Max in Array and Calculate Dot
===
## Find Max in Array
### Naive Solution
T(n) = 2(n-1)
```java=
public int max(){
    int max = A[0];
    for(int i=1; i<A.length; i++)
        if(A[i]>max) max=A[i];
    return max;
}
```
### Divide and Conquer
T(n) ≒ 1.5n
```java=
public int max(){
    int max=A[0];
    for(int i=1; i<A.length-1; i+=2){
        if(A[i]>A[i+1]){
            if(A[i]>max) max=A[i];
        }else{
            if(A[i+1]>max) max=A[i+1];
        }
    }
    if(A.length%2==0){
        if(A[A.length-1]>max) max=A[A.length-1];
    }
    return max;
}
```

## Calculate Dot
T(n) = n
```java=
public int dot(int[] B){
    int sum = 0;
    for(int i=0; i<A.length; i++) sum += A[i]*B[i];
    System.out.println(sum);
    return 0;
}
```
