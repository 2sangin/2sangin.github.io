---
layout: post
title: "Fly me to the Alpha Centauri"
date: "2018-03-30 00:30:27 +0900"
---
# 1DP 1주 4일차
[문제 바로가기](https://www.acmicpc.net/problem/1011)

거리가 1 광년부터 1 광년씩 순차적으로 10 광년까지 가는 동안의 k 값을 나열해보면 아래와 같다.

1  
11  
111  
121  
1211  
1221  
12211  
12221  
12321  
123211  
...

1부터 10 광년까지의 값들 말고도 쭉쭉 써놓고 한참을 보다보니 결국 규칙을 깨달았다.  
우선 당연한거지만 숫자는 한 번에 1씩만 변한다. 12211에서 122211이 되는 것처럼 말이다.  
또한 k 값들 중 최댓값은 가야하는 거리의 제곱근의 정수부분을 넘지 않는다.

가야하는 거리(y - x)를 **d**라고 하고 **√d**의 정수부분을 **c**라 하면,

- d <= c<sup>2</sup>일 때, ___k<sub>n</sub> = 2 * c - 1___
- d - c <= c<sup>2</sup>일 때, ___k<sub>n</sub> = 2 * c___
- d - 2c <= c<sup>2</sup>일 때, ___k<sub>n</sub> = 2 * c + 1___

이 된다.

{% highlight java %}
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class Main {
   public static void main(String[] args) {
      try (BufferedReader reader = new BufferedReader(new InputStreamReader(System.in))) {
         int testcase = Integer.valueOf(reader.readLine());
         int[] counts = new int[testcase];
         for (int i = 0; i < testcase; i++) {
            StringTokenizer st = new StringTokenizer(reader.readLine(), " ");
            int d = -Integer.valueOf(st.nextToken()) + Integer.valueOf(st.nextToken());
            int c = (int) Math.sqrt(d);
            if (d == c * c) {
               counts[i] = 2 * c - 1;
            } else if (d - c <= c * c) {
               counts[i] = 2 * c;
            } else if (d - 2 * c <= c * c) {
               counts[i] = 2 * c + 1;
            }
         }

         BufferedWriter bo = new BufferedWriter(new OutputStreamWriter(System.out));
         for (int i = 0; i < testcase; i++) {
            bo.write(counts[i] + "\n");
         }
         bo.flush();
         bo.close();
      } catch (IOException e) {
         e.printStackTrace();
      }
   }
}
{% endhighlight %}