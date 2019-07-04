# join with () at before and after
また、前後を丸括弧()で囲むことも可能です。

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MyClass {
  public static void main(String args[]) {
    List<String> list = Arrays.asList("en", "ja", "fr", "es", "zh");
    String str = list.stream().collect(Collectors.joining(",", "(", ")"));
    System.out.println(str); // => (en,ja,fr,es,zh)
  }
}
