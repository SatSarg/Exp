# Experimentation
```C#
 int sum=0;
   for(int i=1;i<=n;++i,a++,b++)
   {
       int mult=a*b;
       sum+=mult;          
   }
   return sum;
``` 
   is the similiar
```C#
return Enumerable.Repeat(0, n).Sum(x => a++ * b++);
```
