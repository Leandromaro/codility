# codility
Codility Exercises

// 1 - binaryGap
class Solution {
        LinkedList<Integer> l = new LinkedList<Integer>();
        for(int i : A) {
            l.add(i);
        }
        Integer last = l.getLast();
        l.remove(l.size()-1);

        System.out.println(A);
}

//2.a - Ciclyc

class Solution {
        LinkedList<Integer> l = new LinkedList<Integer>();
        for(int i : A) {
            l.add(i);
        }
        Integer last = l.getLast();
        l.remove(l.size()-1);

        System.out.println(A);
}
//2.b OddNumber
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

// 3.a Frog
class Solution {
    public int solution(int X, int Y, int D) {
        double doubleX = X;
        double doubleY = Y;
        double doubleD = D;
        double div = (doubleY-doubleX)/doubleD;
        return (int) Math.ceil(div);
    }
}

// 3.b PermMissingElement
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
// 3.c TapeEquilibrium
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
// 4.1 FrogRiverSide
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
