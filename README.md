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
####To prepare his students for an upcoming game, the sports coach decides to try some new training drills. To begin with, he lines them up and starts with the following warm-up exercise: when the coach says 'L', he instructs the students to turn to the left. Alternatively, when he says 'R', they should turn to the right. Finally, when the coach says 'A', the students should turn around.

Unfortunately some students (not all of them, but at least one) can't tell left from right, meaning they always turn right when they hear 'L' and left when they hear 'R'. The coach wants to know how many times the students end up facing the same direction.

Given the list of commands the coach has given, count the number of such commands after which the students will be facing the same direction.
```C#
int lineUp(string commands) {
int s = 0;
    bool same = true;
    
    foreach(char c in commands)
    {
        switch(c)
        {
            case 'A':
                break;
            default:
                same ^= true;
                
                break;
        }
        if(same)
            s++;
    }
    
    return s;
}
```
   is the similiar
```C#
int lineUp(string commands) {
int t=1;
    return commands.Select(
            c => t =(c == 'A' ? t : 1-t)).Sum();
```

```C#
int additionWithoutCarrying(int param1, int param2) {
int l1 = param1 >= param2? param1.ToString().Length : param2.ToString().Length;
    int x = 0;

    for (int i = 0; i < l1; i++)
    {
        x = x + ((param1 % 10 + param2 % 10) % 10) * (int)Math.Pow(10, i);
        param1 = param1 / 10;
        param2 = param2 / 10;
    }
    return x;
}
```
is the  similiar
```C#
int additionWithoutCarrying(int param1, int param2) {
    int sum = 0;
    int pos = 1;
    while(param1 > 0 || param2 > 0)
    {
        sum += ((param1+param2)%10)*pos;
        param1 /= 10;
        param2 /= 10;
        pos *= 10;
    }
    return sum;
}
```

#### You have k apple boxes full of apples. Each square box of size m contains m × m apples. You just noticed two interesting properties about the boxes:

The smallest box is size 1, the next one is size 2,..., all the way up to size k.
Boxes that have an odd size contain only yellow apples. Boxes that have an even size contain only red apples.
Your task is to calculate the difference between the number of red apples and the number of yellow apples.

Example

For k = 5, the output should be
appleBoxes(k) = -15.

There are 1 + 3 * 3 + 5 * 5 = 35 yellow apples and 2 * 2 + 4 * 4 = 20 red apples, making the answer 20 - 35 = -15.
```C#
int appleBoxes(int k) {
    int r = 0;
    int y = 1;
    for (int i = 2; i <= k; i++)
    {
        y = i % 2 != 0 ? (y + i * i) : y;
        r = i % 2 != 0 ? r : (r + i * i);
    }
    return r - y;

}
```
is the  similiar
```C#
int appleBoxes(int k) {
    return Enumerable.Range(1,k)
        .Sum(s => (s % 2 == 0 ? 1 : -1) 
            * s*s);
}
```
#### Define an integer's roundness as the number of trailing zeroes in it.

Given an integer n, check if it's possible to increase n's roundness by swapping some pair of its digits.

Example

For n = 902200100, the output should be
increaseNumberRoundness(n) = true.

One of the possible ways to increase roundness of n is to swap digit 1 with digit 0 preceding it: roundness of 902201000 is 3, and roundness of n is 2.

For instance, one may swap the leftmost 0 with 1.

For n = 11000, the output should be
increaseNumberRoundness(n) = false.

Roundness of n is 3, and there is no way to increase it.
```C#
bool increaseNumberRoundness(int n) {
bool bo = false;
    while (n%10 == 0) n = n / 10;
    while (n > 9)
    {
        if (n%10 != 0) n = n / 10;

        else
        {
            bo = true;
            break;
        }
    }

    return bo;
}
```
is the similiar
```C#
bool increaseNumberRoundness(int n) {
    return n.ToString().Reverse()
        .SkipWhile(d => d == '0')
        .SkipWhile(d => d != '0')
        .Any(d => d == '0');
}
```
#### Define an integer's roundness as the number of trailing zeroes in it.

Given an integer n, check if it's possible to increase n's roundness by swapping some pair of its digits.

Example

For n = 902200100, the output should be
increaseNumberRoundness(n) = true.

One of the possible ways to increase roundness of n is to swap digit 1 with digit 0 preceding it: roundness of 902201000 is 3, and roundness of n is 2.

For instance, one may swap the leftmost 0 with 1.

For n = 11000, the output should be
increaseNumberRoundness(n) = false.

Roundness of n is 3, and there is no way to increase it.

```C#
int rounders(int value) {
int e = 1;
    
    while(value / 10 != 0){
        if(value % 10 >= 5){
            value/= 10;
            value++;
        }
        else{
            value/=10;
        }
        e *=10;
    }
    return value*e;
}
```
is the similiar
```C#
int rounders(int value) {
    int lastdigit, powerOf10 = 1;
      
    while (value > 9) {
        lastdigit = value % 10;
        powerOf10 *= 10;
        value /= 10;
        if (lastdigit >= 5)
            value += 1;
        
    }
    
    return value * powerOf10;
}
```


#### When a candle finishes burning it leaves a leftover. makeNew leftovers can be combined to make a new candle, which, when burning down, will in turn leave another leftover.

You have candlesNumber candles in your possession. What's the total number of candles you can burn, assuming that you create new candles as soon as you have enough leftovers?

Example

For candlesNumber = 5 and makeNew = 2, the output should be
candles(candlesNumber, makeNew) = 9.

Here is what you can do to burn 9 candles:

burn 5 candles, obtain 5 leftovers;
create 2 more candles, using 4 leftovers (1 leftover remains);
burn 2 candles, end up with 3 leftovers;
create another candle using 2 leftovers (1 leftover remains);
burn the created candle, which gives another leftover (2 leftovers in total);
create a candle from the remaining leftovers;
burn the last candle.
Thus, you can burn 5 + 2 + 1 + 1 = 9 candles, which is the answer.
```C#
int candles(int candles, int makeNew) {
    int c = 0;
    int l = 0;
    while(candles > 0)
    {
        c += candles;
        l += candles;
        candles = l/makeNew;
        l = l%makeNew;
    }
    return c;
}
```

is similiar
```C#
int candles(int candlesNumber, int makeNew) {
int burned = 0;
    int leftowers = 0;
    while (candlesNumber > 0)
    {
        burned += candlesNumber;
        leftowers += candlesNumber;
        candlesNumber = leftowers / makeNew;
        leftowers %= makeNew;
    }
    return burned;
}
```

#### Imagine a white rectangular grid of n rows and m columns divided into two parts by a diagonal line running from the upper left to the lower right corner. Now let's paint the grid in two colors according to the following rules:

A cell is painted black if it has at least one point in common with the diagonal;
Otherwise, a cell is painted white.
Count the number of cells painted black.

Example

For n = 3 and m = 4, the output should be
countBlackCells(n, m) = 6.

There are 6 cells that have at least one common point with the diagonal and therefore are painted black.



For n = 3 and m = 3, the output should be
countBlackCells(n, m) = 7.

7 cells have at least one common point with the diagonal and are painted black.



```C#
int countBlackCells(int n, int m) {
    
int c = 0;
    int x = 0;

    if (n > m)
    {
        c = (n % m == 0)?(n / m):(n / m + 1);
    }

    if (n < m)
    {
        c = (m % n == 0)?(m / n):(m / n + 1);
    }

    x = (n > m)?(n - 1):((m - 1) * c);

    if (n == m) x = m + 2*(m-1); 


    return x;
}```
