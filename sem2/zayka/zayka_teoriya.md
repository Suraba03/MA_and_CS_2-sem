# __билет 1__ ##################################################################################
## 1.1 Ссылочный тип данный --------------------------- дописать
текст...
## 1.2 Алгоритм Кнута-Морриса-Пратта (КМП)
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП
+ написать префикс функцию, алгоритм -- [вики итмо](https://neerc.ifmo.ru/wiki/index.php?title=Префикс-функция) и [хабр](https://habr.com/ru/post/307220/) 
    + псевдокод 
        ```python
        int[] prefixFunction(string s):
          p[0] = 0
          for i = 1 to s.length - 1
              k = p[i - 1]
              while k > 0 and s[i] != s[k]
                  k = p[k - 1]
              if s[i] == s[k]
                  k++
              p[i] = k
          return p
        ```
+ найти элементы в массиве префиксов длиной в образец, это и есть первые индексы вхождения
    + псевдокод
        ```python
        int[] kmp(string P, string T):
           int pl = P.length
           int tl = T.length
           int[] answer
           int[] p = prefixFunction(P + "#" + T)
           int count = 0
           for i = 0 .. tl - 1
              if p[pl + i + 1] == pl
                 answer[count++] = i
           return answer
        ```


# __билет 2__ ##################################################################################
## 2.1 Деревья выражений ---------------------------- дописать
текст...
## 2.2 Таблицы с прямым доступом (хэш таблицы)
#### теория
+ [хорошее объяснение](https://javarush.ru/quests/lectures/questharvardcs50.level05.lecture06)
+ [код](https://habr.com/ru/post/509220/)
+ [вики итмо](https://neerc.ifmo.ru/wiki/index.php?title=Хеш-таблица)
#### код, полиномиальная хэш-функция с использованием схемы горнера 
```c
int HashFunctionHorner(const char *s[], int table_size, const int key)
{
    int hash_result = 0;
    for (int i = 0; s[i] < strlen(s); i++) {
        hash_result = (key * hash_result + s[i]) % table_size; // итеративное вычисление 
    }                                                          // полинома по схеме Горнера.
    hash_result = (hash_result * 2 + 1) % table_size; // hash_result должно
    return hash_result;                               //  быть взаимопросто с table_size.
}
```











# __билет 3__ ##################################################################################
## 3.1 Вектор. Функциональная спецификация, логическое описание, физическое представление.
текст...
## 3.2 Алгоритм Рутисхаузера
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 4__ ##################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 5__ ##################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 6__ ##################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 7__ ##################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП

# __билет 8__ ##################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 9__ ##################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 10__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 11__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 12__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 13__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 14__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП


# __билет 15__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП



# __билет 16__ #################################################################################
## 1.1
текст...
## 1.2 
#### код на си
##### КМП
[KMP](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/kmp)
##### простая реализация поиска
[Ссылочка](https://github.com/Suraba03/Algorithms-and-Data-Structures/tree/main/find_sample_in_string/simple_find_sample_in_string)
#### пояснение для КМП









