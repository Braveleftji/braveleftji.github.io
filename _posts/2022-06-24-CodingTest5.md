---
title: 코딩테스트 5. 타겟 넘버
author: 꼬낄라
date: 2022-06-24 17:00:00 +0900
categories: [CodingTest, Programmers-Level-2]
tags: [느리지만 확실하게 !, langsam aber sicher,Java]     # TAG names should always be lowercase
---

# 설명

n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
```java
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```
사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

## 제한사항
주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
각 숫자는 1 이상 50 이하인 자연수입니다.
타겟 넘버는 1 이상 1000 이하인 자연수입니다. 사람의 각 회의 가위, 바위, 보 정보가 주어지면 각 회를 누가 이겼는지 출력하는 프로그램을 작성하세요.


## 입출력 예

|numbers|	target|	return|
|---|---|---|
|[1, 1, 1, 1, 1]	|3|	5|
|[4, 1, 2, 1]	|4|	2|

### 입출력 예 설명

### 입출력 예 #1

문제 예시와 같습니다.

### 입출력 예 #2
```java
+4+1-2+1 = 4
+4-1+2-1 = 4
```
- 총 2가지 방법이 있으므로, `2`를 `return` 합니다.

-----
# 풀이
```java
class Solution {
    public int solution(int[] numbers, int target) {
        dfs(numbers, target, 0, 0);
        int answer = 0;
        return answer;
    }

    public int dfs(int[] numbers, int target, int depth, int result) {
        int count = 0;
        if (numbers.length == depth) {
            if (result == target) {
                return 1;
            } else return 0;
        }
        count += dfs(numbers, target, depth + 1, result + numbers[depth]);
        count += dfs(numbers, target, depth + 1, result - numbers[depth]);
        return count;
    }

    public static void main(String[] args) {
        Solution s = new Solution();
        int[] numbers = {1, 1, 1, 1, 1};
        int target = 3;
        System.out.println(s.solution(numbers, target));
    }
}
```
