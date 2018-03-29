---
layout: post
title: "디지털 카운터"
date: "2018-03-26 01:06:03 +0900"
---
# 1DP 1주 1일차
[문제 바로가기](https://www.acmicpc.net/problem/1020)

논리회로 때 그레이 코드로 7 세그먼트 구현 하는 게 신기해서 기억에 남았었다.
그래서 제목보고 7 세그먼트 관련 된건가 해서 눌러봤는데 직접적으로 관련은 없더라…
어쨌든 쉬워보여서 골랐음.

무작정 1초씩 증가 시켜서 갯수를 세면 되는 거 아닌가? brute force로 간다.
그런데 런타임 에러가 난다…
입력 값의 길이가 15 자리일 수 있다는 부분을 그냥 넘어갔다. 그래서 origin, maximum을 long으로 바꿨는데 이제는 시간 초과가 난다. 역시 brute force로는 못 할 게 없으니 이런 건 알고리즘으로 치면 안될 것 같다. 앞으로는 아예 brute force는 지양하자…

시간이 흐를 때 앞자리는 거의 변화가 없다는 점을 이용해야 할 것 같은데 확실한 방법이 안 떠오른다. 일단 재귀 호출을 통해서 해보려고 했는데 구현할 방법이 잘 안 떠오르는데 아무래도 이건 아닌가? 첫날부터 너무 어려운 걸 고른 건가…ㅠㅠ 느낌적인 느낌으로는 어려울 것 같지 않아서 골랐는데 다음에 시간 날 때마다 다시 시도해봐야겠다.

{% highlight java linenos %}
import java.util.Scanner;

public class Main {
  private static final int[] NUMBERS_LINE = {6, 2, 5, 5, 4, 5, 6, 3, 7, 5};

  public static void main(final String[] args) {

    try (final Scanner scanner = new Scanner(System.in)) {
      final String input = scanner.nextLine();
      final int N = input.length();
      final String format = "%0" + N + "d";
      final int target = countLines(input);
      final long origin = Long.valueOf(input);
      final long maximum = (int) Math.pow(10, N) - 1;

      int elapsedTime = 1;
      while (target != countLines(String.format(format, (origin + elapsedTime) % maximum))) {
        elapsedTime++;
      }
      System.out.println(elapsedTime);
    }
  }

  private static int countLines(final String number) {
    int target = 0;
    for (int i = 0; i < number.length(); i++) {
      target += NUMBERS_LINE[number.charAt(i) - '0'];
    }
    return target;
  }
}
{% endhighlight %}