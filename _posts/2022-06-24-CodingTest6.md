---
title: 코딩테스트 6. 단어 변환
author: 꼬낄라
date: 2022-06-24 17:00:00 +0900
categories: [CodingTest, Programmers-Level-2]
tags: [느리지만 확실하게 !, langsam aber sicher,Java]     # TAG names should always be lowercase
---
# 설명
두 개의 단어 `begin`, `target`과 단어의 집합 `words`가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. `words`에 있는 단어로만 변환할 수 있습니다.
   예를 들어 `begin`이 "hit", `target`가 `"cog"`, `words`가 `["hot","dot","dog","lot","log","cog"]`라면 `"hit"` -> `"hot"` -> `"dot"` -> `"dog"` -> `"cog"`와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 `begin`, `target`과 단어의 집합 `words`가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 `begin`을 `target`으로 변환할 수 있는지 `return` 하도록 `solution` 함수를 작성해주세요.

## 제한사항
각 단어는 알파벳 소문자로만 이루어져 있습니다.
각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
`words`에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
`begin`과 `target`은 같지 않습니다.
변환할 수 없는 경우에는 `0`를 `return` 합니다.
## 입출력 예

|begin	|target	|words	|return|
|---|---|---|---|
|"hit"	|"cog"	|["hot", "dot", "dog", "lot", "log", "cog"]	|4|
|"hit"	|"cog"	|["hot", "dot", "dog", "lot", "log"]	|0|

## 입출력 예 설명
### 예제 #1
문제에 나온 예와 같습니다.

### 예제 #2
`target`인 `"cog"`는 `words` 안에 없기 때문에 변환할 수 없습니다.

-----
# 풀이
```java
class Solution {
    public int solution(String begin, String target, String[] words) {
        int answer = Integer.MAX_VALUE;
        boolean[] visited = new boolean[words.length];
        answer = dfs(begin, target, words, visited, 1, answer);
        return answer;
    }

    public int dfs(String begin, String target, String[] words, boolean[] visited, int count, int answer) {
        if (begin.equals(target)) {
            return count - 1;
        }
        for (int i = 0; i < words.length; i++) {
            int beginToWord = 0;
            if (!begin.equals(words[i]) && !visited[i]) {
                for (int j = 0; j < begin.length(); j++) {
                    if (words[i].charAt(j) != begin.charAt(j)) {
                        beginToWord++;
                    }
                }
                if (beginToWord == 1) {
                    visited[i] = true;
                    answer = Math.min(answer, dfs(words[i], target, words, visited, count + 1, answer));
                    visited[i] = false;
                }
            }
        }
        return answer;
    }
    
    public static void main(String[] args) {
        Solution s = new Solution();
        String begin = "hit";
        String target = "cog";
        String[] words = {"hot", "dot", "dog", "lot", "log", "cog"};
        System.out.println(s.solution(begin, target, words));
    }
}
```
