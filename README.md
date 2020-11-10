# arithmetic-_operations_using_various-_threads_openmp
#include<stdio.h>
#include<omp.h>
#include<math.h>
#include<iostream>
void add(int a,int b)
{
float sum = a+b;
printf("Sum of numbers %d and %d is %f\n", a, b, sum);
}
void subtract(int a,int b)
{
float difference = a-b;
printf("Difference of numbers %d and %d is %f\n", a, b, difference);
}
void multiply(int a,int b)
{
float multiplication = a*b;
printf("Multiplication of numbers %d and %d is %f\n", a, b, multiplication);
}
void divide(int a,int b)
{
float division = a/b;
printf("Division of number %d by %d is %f\n", a, b, division);
}
int main()
{
int a, b;
float sum, difference, multiplication, division, start, end;
a = 40;
b = 4;

start = omp_get_wtime();
#pragma omp parallel num_threads(4) default(none) shared(a,b)
{
int threadId = omp_get_thread_num();
switch(threadId)
{
case 0:
add(a,b);
break;
case 1:
subtract(a,b);
break;
case 2:
multiply(a,b);
break;
case 3:
divide(a,b);
break;
}
}
end = omp_get_wtime();
printf("Total time taken in parallel block is %f seconds", end-start);
return 0;
}
