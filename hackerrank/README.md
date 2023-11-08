# Самые интересные задачи из курса hackerrank "10 days of statistics"

## (1) Mean, Median and Mode
 Given an array, , of  integers, calculate and print the respective mean, median, and mode on separate lines. If your array contains more than one modal value, choose the numerically smallest one.

```
def mode(list):
    return max(sorted(set(list)), key=list.count)
def mean(list):
    return(sum(list) / len(list))
def median(list):
    n = len(list)
    list = sorted(list)
    return (list[n//2] if n % 2 else (list[n//2-1] + list[n//2]) / 2)
    
n = int(input())
arr = list(map(int, input().split()))

print(mean(arr), median(arr), mode(arr), sep='\n')
```

## (2) Interquartile range
Given an array, , of  integers and an array, , representing the respective frequencies of 's elements, construct a data set, , where each  occurs at frequency . Then calculate and print 's interquartile range, rounded to a scale of  decimal place (i.e.,  format).

```
def interQuartile(values, freqs):
    arr = []
    
    for i in range(len(values)):
        arr += freqs[i] * [values[i]]
    
    n=len(arr)
    
    arr.sort()
    t = int(len(arr)/2)
    
    if len(arr)%2==0:
        L = arr[:t]
        U = arr[t:]
    else:
        L = arr[:t]
        U = arr[t+1:]
    
    q1 = float(median(L))
    q3 = float(median(U))
    
    print(round(q3 - q1, 1))
```

## (3) Standart deviation
 Given an array, , of  integers, calculate and print the standard deviation. 

```
def stdDev(arr):
    mean = sum(arr) / len(arr)
    
    sq_sum_of_dev = 0
    for i in arr:
        sq_sum_of_dev += (i - mean) ** 2
        
    print(round((sq_sum_of_dev / len(arr)) ** 0.5, 1)) 
```

## (4) Binomial Distribution
A manufacturer of metal pistons finds that, on average,  of the pistons they manufacture are rejected because they are incorrectly sized. What is the probability that a batch of  pistons will contain:

- No more than  rejects?
- At least  rejects?

```
def fact(n):
    return 1 if n <= 1 else n * fact(n - 1)

def comb(n, x):
    return fact(n) / (fact(x) * fact(n - x))

def b(x, n, p):
    return comb(n, x) * p ** x * (1 - p) ** (n - x)


l, r = list(map(float, input().split(" ")))
print(round(sum([b(i, r, l / 100) for i in range(0, 3)]), 3))
print(round(sum([b(i, r, l / 100) for i in range(2, 11)]), 3))
```

## (5) Normal Distribution
The final grades for a Physics exam taken by a large group of students have a mean of  and a standard deviation of . If we can approximate the distribution of these grades by a normal distribution, what percentage of the students:

Scored higher than  (i.e., have a )?
Passed the test (i.e., have a )?
Failed the test (i.e., have a )?

```
import math
mean, std = 70, 10
cdf = lambda x: 0.5 * (1 + math.erf((x - mean) / (std * (2 ** 0.5))))

print(round((1 - cdf(80)) * 100, 2))
print(round((1 - cdf(60)) * 100, 2))
print(round((cdf(60)) * 100, 2))
```

## (6) The central limit theoram
The number of tickets purchased by each student for the University X vs. University Y football game follows a distribution that has a mean of  and a standard deviation of .

A few hours before the game starts,  eager students line up to purchase last-minute tickets. If there are only  tickets left, what is the probability that all  students will be able to purchase tickets?

```
import math

x = int(input())
n = int(input())
mu = float(input())
sigma = float(input())

mean = n * mu 
std = math.sqrt(n) * sigma

cdf = lambda x: 0.5 * (1 + math.erf((x - mean) / (std * (2 ** 0.5))))

print(round(cdf(x), 4))

```
