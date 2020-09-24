# codility
Codility Exercises

## 1 - binaryGap
```
class Solution {
   public int solution(int N) {
        String binaryString = Integer.toBinaryString(N);
        String[] binaryArray = binaryString.split("");
        int max = 0;
        int count = 0;
        for (String i : binaryArray){
            if(i.equals("1")){
                if(count>max){
                    max = count;
                }
                count = 0;
            }else {
                count++;
            }
        }
  }
}
```

## 2.a - Ciclyc
```
class Solution {
        LinkedList<Integer> l = new LinkedList<Integer>();
        for(int i : A) {
            l.add(i);
        }
        Integer last = l.getLast();
        l.remove(l.size()-1);

        System.out.println(A);
}
```
## 2.b OddNumber
```
class Solution {
    public int solution(int[] A) {
        Map<Integer, Long> collect = Arrays.stream(A)
                .boxed()
                .collect(Collectors.groupingBy(e -> e, Collectors.counting()));

        Optional<Map.Entry<Integer, Long>> entry = collect.entrySet()
                .stream()
                .filter(v -> v.getValue().equals(1l))
                .findAny();
        if(entry.isPresent()){
            return entry.get().getKey();
        }
        return 0; 
    }
}
```
## 3.a Frog
```
class Solution {
    public int solution(int X, int Y, int D) {
        double doubleX = X;
        double doubleY = Y;
        double doubleD = D;
        double div = (doubleY-doubleX)/doubleD;
        return (int) Math.ceil(div);
    }
}
```

## 3.b PermMissingElement
```
 public static int solution(int[] A) {
        if(A.length == 0) return 1;

        int sumArr = 0;

        for(int i=0; i < A.length; i++){
            sumArr = sumArr + A[i];
        }

        int sumN = 0;

        for(int i=1; i <= A.length+1; i++){
            sumN = sumN + i;
        }

        if(sumArr == sumN)  return A.length;
        return  sumN - sumArr;
    }
```
## 3.c TapeEquilibrium
```
public int solution(int[] A) {
        long sumAllElements = 0;
        for(int i=0; i<A.length; i++) {
            sumAllElements += A[i];
        }

        int minDifference = Integer.MAX_VALUE;
        int currentDifference = Integer.MAX_VALUE;
        long sumFirstPart = 0;
        long sumSecondPart = 0;

        for(int p=0; p<A.length-1; p++) {
            sumFirstPart += A[p];
            sumSecondPart = sumAllElements - sumFirstPart;
            currentDifference = (int) Math.abs(sumFirstPart - sumSecondPart);
            minDifference = Math.min(currentDifference, minDifference);
        }
        return minDifference;
    }
```
## 4.1 FrogRiverSide
```
class Solution {
    public int solution(int X, int[] A) {
        int steps = X;
        boolean[] bitmap = new boolean[steps+1];
        for(int i = 0; i < A.length; i++){
            if(!bitmap[A[i]]){
                bitmap[A[i]] = true;
                steps--;
                if(steps == 0) return i;
            }

        }
        return -1;
    }
}
```
## 4.2 MaxCounter
```
 // Result -> 77% 
 // Complexity O(N2)
  public static int[] solution(int N, int[] A) {
        int[] counters = new int[N];
        int maxValue = 0;
        for (int operation : A) {
            if (operation > N) {
                Arrays.fill(counters, maxValue);
            } else {
                counters[operation - 1]++;
                if (counters[operation - 1] > maxValue) {
                    maxValue = counters[operation - 1];
                }
            }
        }
        return counters;
    }
```
```
// Result -> 100%
// Avoid consecutives for O(N2) using two separates for statements we get linear complexity 
 public static int[] solution(int N, int[] A) {
        int result[] = new int[N];
        int lastUpdate = 0;
        int length = A.length;
        int maxValue = 0;
        for (int i=0; i<length;i++){
            int operation = A[i];
            if(operation > N){
                lastUpdate = maxValue;
            }else{
                int position = operation - 1;
                if (result[position] < lastUpdate)
                    result[position] = lastUpdate + 1;
                else{
                    result[position]++;
                }
                if (result[position] > maxValue) {
                    maxValue = result[position];
                }
            }
        }
        for (int iii = 0; iii < N; iii++) {
            if (result[iii] < lastUpdate)
                result[iii] = lastUpdate;
        }
        return result;
    }
```
## 4.3 Missing Integer 
```
public static int solution(int[] A) {
        int smallestMissingInteger = 1;
        if (A.length == 0) {
            return smallestMissingInteger;
        }
        Set<Integer> set = new HashSet<Integer>();
        for (int value : A) {
            if (value > 0) {
                set.add(value);
            }
        }
        while (set.contains(smallestMissingInteger)) {
            smallestMissingInteger++;
        }
        return smallestMissingInteger;
    }
```
## 4.4 PermCheck
```
public static int solution(int[] A) {
        Set<Integer> value = Arrays
        .stream(A)
        .boxed()
        .collect(Collectors.toCollection(HashSet::new));
        
        Integer count = 1;

        while (value.contains(count)){
            count++;
        }
        
        Integer flag = count - 1;
        
        if(flag.equals(A.length)){
           return 1;
        }
        return 0;
}
```
## 5.1 CountDiv
```
   public int solution(int A, int B, int K) {
        return B / K - A / K + (A % K == 0 ? 1 : 0);
    }
```
## 5.2 GenomicRangeQuery
```
   public static int[] solution(String S, int[] P, int[] Q){
        CharSequence charSequence;
        int length = P.length;
        int[] result = new int[length];
        for (int i=0; i<length; i++){
            int left = P[i];
            int right = Q[i]+1;
            charSequence = S.subSequence(left, right);
            String[] segment = charSequence.toString().split("");

            int countA, countC, countG, countT = 0;
            countA = (int) Arrays.stream(segment).filter(s -> s.equals("A")).count();
            countC = (int) Arrays.stream(segment).filter(s -> s.equals("C")).count();
            countG = (int) Arrays.stream(segment).filter(s -> s.equals("G")).count();
            countT = (int) Arrays.stream(segment).filter(s -> s.equals("T")).count();

            int min = 0;
            if(countA>0){
                min = 1;
            }else if(countC>0){
                min = 2;
            }else if(countG>0){
                min = 3;
            }else if(countT>0){
                min = 4;
            }
            result[i] = min;

        }
        return result;
    }
```

## 6.1 Distinct
```
   public static int solution(int[] A) {
       return Arrays
                .stream(A)
                .boxed()
                .collect(Collectors.toSet())
                .size();
    }
```
## 7.1 Brackets

```
class Solution {
    public int solution(String S) {
        Deque<Character> stack = new ArrayDeque<Character>();

        for(int i = 0; i < S.length(); i++) {
            char c = S.charAt(i);

            switch (c) {
                case ')':
                    if (stack.isEmpty() || stack.pop() != '(')
                        return 0;
                    break;
                case ']':
                    if (stack.isEmpty() || stack.pop() != '[')
                        return 0;
                    break;
                case '}':
                    if(stack.isEmpty() || stack.pop() != '{')
                        return 0;
                    break;
                default:
                    stack.push(c);
                    break;
            }
        }

        return stack.isEmpty() ? 1 : 0;
    }
}
```

## 8.1 
Difference between HashMap, LinkedHashMap and TreeMap

All three classes implement the Map interface and offer mostly the same functionality. The most important difference is the order in which iteration through the entries will happen:

HashMap makes absolutely no guarantees about the iteration order. It can (and will) even change completely when new elements are added.
TreeMap will iterate according to the "natural ordering" of the keys according to their compareTo() method (or an externally supplied Comparator). Additionally, it implements the SortedMap interface, which contains methods that depend on this sort order.
LinkedHashMap will iterate in the order in which the entries were put into the map
"Hashtable" is the generic name for hash-based maps. In the context of the Java API, Hashtable is an obsolete class from the days of Java 1.1 before the collections framework existed. It should not be used anymore, because its API is cluttered with obsolete methods that duplicate functionality, and its methods are synchronized (which can decrease performance and is generally useless). Use ConcurrentHashMap instead of Hashtable.

```
public int solution(int[] A) {
        int average = A.length / 2;
        int moreThanAverage = average + 1;
        Map<Integer, Long> collect = Arrays
                .stream(A)
                .boxed()
                .collect(Collectors.groupingBy(e -> e.hashCode(), TreeMap::new, Collectors.counting()));
        Optional<Integer> dominator = collect.keySet()
                .stream()
                .filter(k -> collect.get(k).intValue() >= moreThanAverage)
                .findAny();
        if (dominator.isPresent()) {
            int count = 0;
            while (count < A.length) {
                if (A[count] == dominator.get()) {
                    return count;
                }
                count++;
            }
        }
        return -1;
    }

```
## 9.1 Max Two Slides

### Maximum subarray problem

Let’s look at the picture below and make some key observations.

![alt text](https://bogdankotzev.com/wp-content/uploads/2018/07/MaxDoubleSliceSum1.png)


After digesting the equation for the problem, The sum of double slice (X, Y, Z) is the total of A[X + 1] + A[X + 2] + … + A[Y − 1] + A[Y + 1] + A[Y + 2] + … + A[Z − 1], we can simply see that the problem can be separated into two subarrays. The minimum value for our slice is always 0, because consecutive numbers such as (2,3,4) will yield 0 + 0 = 0.

The first subarray called leftHalf is from [1, Y).

The second subarray called rightHalf is from (Y, N – 1].

To solve the problem, we maximize the left slice, then we maximize the right slice and combine them. In the example above the maximized left slice is 2 + 6 = 8, and the maximized right slice is 4 + 5 = 9. This gives us 8 + 9 = 17.

Now of course, we know this is the correct answer by the problem description, but in reality we are checking the max double slice for Y between [1,N-1].

The code below works like this:

Go through array A and store the maximized leftHalf into an array for later use.
Go through array A and calculate the maximized rightHalf
As soon as rightHalf is calculated we can use it in combination with the previously stored leftHalf result to calculate our maxSlice
NOTE: The tricky part is figuring out which value in our array goes with our current rightHalf.
```
// number of elements in A
        int N = A.length;
        // variable representing the maximum slice
        int maxSlice = 0;
        // holds the results for the left half calculations
        int [] leftHalfResults = new int [N];
        // used for calculation of the right half
        int rightHalf = 0;

        // maximum slice of the first half
        // starts at 1, because our value at index 0 is always going to be 0
        // ends at N-2, because that is the maximum size for our left half
        // leftHalfResults[0] = 0;
        for (int k = 1; k < N-2; k++) {
            leftHalfResults[k] = Math.max(0, leftHalfResults[k-1] + A[k]);
        }


        // calculate the maximum right half
        // At the same time calculate the maximum slice for the current leftHalf and rightHalf combination
        for (int i = N-1; i > 1 ; i--) {
            // the tricky part was to figure out what k should be to make sure the two halves correspond to the same midpoint
            // this took some time to do using System.out.println()
            int k = i-2;
            // when the right half is 0
            if (i == N-1) {
                rightHalf = 0;
            }
            else {
                rightHalf = Math.max(0, rightHalf + A[i]);
            }
            maxSlice = Math.max(maxSlice, leftHalfResults[k] + rightHalf);
        }

        return maxSlice;
```

## 14.1 Binary - MinMax Solution
```
class Solution {
   public int solution(int K, int M, int[] A) {
       // write your code in Java SE 8
       int high = sum(A);
       int low = max(A);

       int mid = 0;

       int smallestSum = 0;

       while (high >= low) {
           mid = (high + low) / 2;
           int numberOfBlock = blockCount(mid, A);

           if (numberOfBlock > K) {
               low = mid + 1;
           } else if (numberOfBlock <= K) {
               smallestSum = mid;
               high = mid - 1;
           }

       }
       return smallestSum;
   }

   public int sum(int[] A) {
       int total = 0;
       for (int i = 0; i < A.length; i++) {
           total += A[i];
       }
       return total;
   }

   public int max(int[] A) {
       int max = 0;
       for (int i = 0; i < A.length; i++) {
           if (max < A[i]) max = A[i];
       }
       return max;
   }

   public int blockCount(int max, int[] A) {
       int current = 0;
       int count = 1;
       for (int i = 0; i< A.length; i++) {
           if (current + A[i] > max) {
               current = A[i];
               count++;
           } else {
               current += A[i];
           }
       }
       return count;
   }
}
```
Explanation:
So what the code does is using a form of binary search. It also uses an example quite similar to your problem.). Where you search for the minimum sum every block needs to contain. In the example case, you need the divide the array in 3 parts

When doing a binary search you need to define 2 boundaries, where you are certain that your answer can be found in between. Here, the lower boundary is the maximum value in the array (lower). For the example, this is 5 (this is if you divide your array in 7 blocks). The upper boundary (upper) is 15, which is the sum of all the elements in the array (this is if you divide the array in 1 block.)

Now comes the search part: In solution() you start with your bounds and mid point (10 for the example). In calculateBlockCount you count (count ++ does that) how many blocks you can make if your sum is a maximum of 10 (your middle point/ or maxSum in calculateBlockCount).
For the example 10 (in the while loop) this is 2 blocks, now the code returns this (blocks) to solution. Then it checks whether is less or more than K, which is the number of blocks you want. If its less than K your mid point is high because you're putting to many array elements in your blocks. If it's more than K, than your mid point is too high and you're putting too little array elements in your array. Now after the checking this, it halves the solution space (upper = mid-1). This happens every loop, it halves the solution space which makes it converge quite quickly.

Now you keep going through your while adjusting the mid, till this gives the amount blocks which was in your input K.
```
Mid =10 , calculateBlockCount returns 2 blocks
solution. 2 blocks < K so upper -> mid-1 =9, mid -> 7  (lower is 5)
Mid =7 , calculateBlockCount returns 2 blocks  
solution() 2 blocks < K so upper -> mid-1 =6, mid -> 5 (lower is 5, cast to int makes it 5)
Mid =5 , calculateBlockCount returns 4 blocks
solution() 4 blocks < K so lower -> mid+1 =6, mid -> 6  (lower is 6, upper is 6
Mid =6 , calculateBlockCount returns 3 blocks
So the function returns mid =6....
```
