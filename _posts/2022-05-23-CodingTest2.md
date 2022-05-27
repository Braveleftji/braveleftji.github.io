---
title: 코딩테스트 2. 숫자열과 영단어
author: 꼬낄라
date: 2022-05-26 17:00:00 +0900
categories: [CodingTest, Programmers-Level-1]
tags: [느리지만 확실하게 !, langsam aber sicher,Java]     # TAG names should always be lowercase
---

문제 설명
====
네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

- 1478 → "one4seveneight"
- 234567 → "23four5six7"
- 10203 → "1zerotwozero3"

이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. `s`가 의미하는 원래 숫자를 `return` 하도록 `solution` 함수를 완성해주세요.

참고로 각 숫자에 대응되는 영단어는 다음 표와 같습니다.

|숫자|	영단어|
|:---|:---|
|0	|zero|
|1	|one|
|2	|two|
|3	|three|
|4	|four|
|5	|five|
|6	|six|
|7	|seven|
|8	|eight|
|9	|nine|

## 제한사항

`1 ≤ s의 길이 ≤ 50`

`s`가 `zero` 또는 `0`으로 시작하는 경우는 주어지지 않습니다.
`return` 값이 `1` 이상 `2,000,000,000` 이하의 정수가 되는 올바른 입력만 `s`로 주어집니다.
입출력 예

|s	                |result|
|:---|:---|
|"one4seveneight"|	1478|
|"23four5six7"|	    234567|
|"2three45sixseven"|	234567|
|"123"|	123|

# 입출력 예 설명
## 입출력 예 #1

문제 예시와 같습니다.
## 입출력 예 #2

문제 예시와 같습니다.
## 입출력 예 #3

`three`는 `3`, `six`는 `6`, `seven`은 `7`에 대응되기 때문에 정답은 입출력 예 #2와 같은 `234567이` 됩니다.
입출력 예 #2와 #3과 같이 같은 정답을 가리키는 문자열이 여러 가지가 나올 수 있습니다.
## 입출력 예 #4

s에는 영단어로 바뀐 부분이 없습니다.
제한시간 안내
정확성 테스트 : 10초

-----
# 풀이
```java
import java.util.Arrays;
import java.util.HashMap;

public class solution {
    public int solution(String s) {
    String answerStr = "";
    HashMap<String,String> temp = new HashMap<>();
        temp.put("zero","0");
        temp.put("one","1");
        temp.put("two","2");
        temp.put("three","3");
        temp.put("four","4");
        temp.put("five","5");
        temp.put("six","6");
        temp.put("seven","7");
        temp.put("eight","8");
        temp.put("nine","9");
        String tempStr="";
        String[] sArray = s.split("");
        for(int i=0; i<sArray.length;i++){
            if (sArray[i].matches("[a-z]")){
                tempStr+=sArray[i];
                if(temp.containsKey(tempStr)){
                    answerStr+=temp.get(tempStr);
                    tempStr="";
                }
            }else if(sArray[i].matches("[0-9]")){
                answerStr+=sArray[i];
            }
        }
    int answer = Integer.parseInt(answerStr);
        return answer;
    }

    public static void main(String[] args) {
        solution ss = new solution();
        ss.solution("one4seveneight");
    }
}
/*
//replaceAll을 깜빡했다..
    String[] arr = {"zero","one","two","three","four","five","six","seven","eight","nine"};
    for (int i = 0; i < arr.length; i++) {
        s.replaceAll(arr[i],String.valueOf(i));
    }
    answer = Integer.parseInt(s);
//이런식으로 해도될듯
*/

```
