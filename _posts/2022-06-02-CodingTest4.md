---
title: 코딩테스트 4. 섬나라 아일랜드
author: 꼬낄라
date: 2022-06-02 17:00:00 +0900
categories: [CodingTest, Inflearn]
tags: [느리지만 확실하게 !, langsam aber sicher,Java]     # TAG names should always be lowercase
---


# 문제 설명

`N*N`의 섬나라 아일랜드의 지도가 격자판의 정보로 주어집니다.

각 `섬은 1`로 표시되어 상하좌우와 대각선으로 연결되어 있으며, `0은 바다`입니다.

섬나라 아일랜드에 몇 개의 섬이 있는지 구하는 프로그램을 작성하세요.


![img](/img/CodingTest4/img1.png)

만약 위와 같다면 섬의 개수는 `5개`입니다.


## 입력
첫 번째 줄에 자연수 `N(3<=N<=20)`이 주어집니다.

두 번째 줄부터 격자판 정보가 주어진다.


## 출력
첫 번째 줄에 섬의 개수를 출력한다.

---
## 예시 입력 1 
```
7
1 1 0 0 0 1 0
0 1 1 0 1 1 0
0 1 0 0 0 0 0
0 0 0 1 0 1 1
1 1 0 1 1 0 0
1 0 0 0 1 0 0
1 0 1 0 1 0 0
```
## 예시 출력 
```
1
```


-----
# 풀이
```java


import java.util.Scanner;

public class Solution {
    int[] dx={0,1,1,1,0,-1,-1,-1}; //x방향 움직임
    int[] dy={-1,-1,0,1,1,1,0,-1}; //y방향 움직임

    //dfs를 통해 섬의 경계 확인
    public void dfs(int x, int y, int[][] board){
        if (x< 0|| y< 0|| x>= board.length|| y>= board.length)return;
        if(!(board[x][y]==0)){
            for (int i = 0; i < dx.length; i++) {
                board[x][y]=0; //방문한 지역은 0으로 변경하여 재방문 X
                dfs(x+dx[i],y+dy[i],board);
            }
        }
    }
    public static void main(String[] args){
        Solution s = new Solution();
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] board = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = sc.nextInt();
            }
        }
        int answer=0;
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j]==1) {
                    answer++; //섬을 찾으면 +1;
                    s.dfs(i, j, board); //섬의 경계 확인 및 0변환
                }
            }
        }
        System.out.println(answer);
    }
}
```
