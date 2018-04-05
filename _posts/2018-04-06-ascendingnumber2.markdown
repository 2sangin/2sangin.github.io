---
layout: post
title: "#7 11057번: 오르막 수 2트"
date: "2018-04-06 00:57:14 +0900"
---
# 1DP 2주 7일차
[문제 바로가기](https://www.acmicpc.net/problem/11057 "11057번: 오르막 수")

[다른 버전 소스코드](https://github.com/atmost1815/1dp/blob/e6bd80135f08c5c33be76e1f6aa150bc9b965558/src/io/github/atmost1815/acmicpc/ascendingnumber/Main.java)

{% highlight java %}
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.util.NoSuchElementException;
import java.util.StringTokenizer;
import java.util.stream.IntStream;

public class Main {
    private static Scanner sc = new Scanner(System.in);

    public static void main(final String[] args) {
        IntStream.of(
                IntStream.of(sc.nextInt())
                        .flatMap(tc -> IntStream.rangeClosed(tc + 1, tc + 9))
                        .reduce(1, (left, right) -> left * right % 10_007))
                .map(v -> v * 6995 % 10_007)
                .forEach(System.out::print);
    }

    static class Scanner {
        private BufferedReader reader;
        private StringTokenizer tokenizer;

        Scanner(final InputStream is) {
            this.reader = new BufferedReader(new InputStreamReader(is));
        }

        String next() {
            if (this.tokenizer == null || !this.tokenizer.hasMoreTokens()) {
                try {
                    this.tokenizer = new StringTokenizer(this.reader.readLine());
                } catch (final IOException e) {
                    throw new NoSuchElementException(e.getMessage());
                }
            }
            return this.tokenizer.nextToken();
        }

        int nextInt() {
            return Integer.parseInt(next());
        }
    }
}
{% endhighlight %}