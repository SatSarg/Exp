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
