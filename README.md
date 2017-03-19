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
