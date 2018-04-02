---
layout: post
title: "붕어빵 판매하기"
date: "2018-04-02 23:55:14 +0900"
---
# 1DP 2주 5일차
[문제 바로가기](https://www.acmicpc.net/problem/11052 "11052번: 붕어빵 판매하기")

붕어빵 N개를 팔았을 때의 최대 수익을 DP[N]이라고 하자.

> DP[1] = 1개 세트 판매 가격  
> DP[2] = 2개 세트 판매 가격 or DP[1] + DP[1]  
> DP[3] = 3개 세트 판매 가격 or DP[2] + DP[1]  
> DP[N] = N개 세트 판매 가격 or DP[N-N/2] + DP[N/2] ...

위와 같이 된다. 참고로 DP[N]일 때 N-1이라든지 2/N-1이 없는 이유는 DP[N-1]이나 DP[2/N-1]에서 이미 거쳐오기 때문이다.

{% highlight java %}
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
  public static void main(final String[] args) throws Exception {
    final BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    final int count = Integer.parseInt(reader.readLine());
    final int[] dp = new int[count + 1];

    final StringTokenizer st = new StringTokenizer(reader.readLine());
    for (int i = 1; i <= count; i++) {
      dp[i] = Integer.parseInt(st.nextToken());
    }

    for (int i = 1; i <= count; i++) {
      for (int j = i / 2; j > 0; j--) {
        dp[i] = Math.max(dp[i - j] + dp[j], dp[i]);
      }
    }
    System.out.println(dp[count]);
  }
}
{% endhighlight %}

ps. 근데 다른 Java 소스 중에 빠르게 돈 걸 참고해서 비슷하게 해봤는데 거의 2배 차이가 좁혀지지 않는다. 그래서 빠르게 하는 건 그냥 포기하고 중복되는 코드를 줄였음.