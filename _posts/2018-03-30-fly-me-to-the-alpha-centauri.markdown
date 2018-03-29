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

1부터 10 광년까지의 값들 말고도 쭉쭉 써놓고 한참을 보다보니 결국 규칙을 깨달았다. (위에 나열한 방식이 아닐 경우 최소 횟수로 이동 할 수 없다.)  
한 번의 공간이동으로 이동 할 수 있는 최대 거리는 총 거리의 제곱근의 정수부분을 넘을 수 없다. 즉, 9 광년의 거리가 안 되는데 3 광년을 이동할 경우에는 마지막 공간이동의 거리가 1 광년이어야 한다는 조건을 달성 할 수 없다.  
  9 광년일 때를 보면 3 광년을 이동하는 경우가 최초로 나오게 되고, 다음 10 광년에서는 늘어난 1 광년을 더 이동하려면 1 광년짜리 공간이동 횟수가 늘어날 수 밖에 없다. 즉, 한 번에 이동할 수 있는 최대 거리인 3 광년을 이동한 경우마다 공간이동 횟수가 1회 늘어나게 된다.

계속 쓰다보니 지치니까 더 이상의 자세한 설명은 생략한다. 수평선을 그리면 이해하기 쉽다.  
어쨌든 결론은 아래다.

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