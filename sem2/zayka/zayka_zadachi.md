# __билет 1__ -- масимальная степень вершины дерева общего вида

#### __Код__

```c
//описание структуры дерева
typedef struct node {
    int key;
    struct node *son;
    struct node *brother;
} tree;

// процедура
void degree(tree *root, int *h, int count)
{
    if (root != NULL) {
        if (count > *h) {
            *h = count;
        }
        degree(root->brother, h, count + 1);
        degree(root->son, h, 0);
    }
}

int main()
{
    ...
    int h = 0;
    degree(kor, &h, 0);
    printf("tree's degree = %d\n", h + 1);
    ...
}
```
#### __пояснение__
+ _переменные_
  + ```tree *root``` -- корень дерева
  + ```h + 1``` -- масимальная степень дерева на данный момент
  + ```count``` -- количество братьев на данный момент
+ _при сравнении_ ```if (count > *h)``` обновляем максимальную степень дерева
+ _шаг рекурсии_
  + ```degree(root->brother, h, count + 1);``` -- переход к брату
  + ```degree(root->son, h, 0);``` -- переход к сыну (брата)
+ _база рекурсии_
  + ```root->son == NULL``` и ```root->brother == NULL```






# __билет 2__ -- сравнение двух линейных списков на указателях

#### __Код__

```c
typedef struct node { // описание структуры узла списка на указателях
    int key;
    struct node *next;
} node;

typedef struct _list { // описание структуры списка на указателях
    int size;
    struct node *head;
} list;

bool check (list * a, list * b) // функция сравнения двух линейных списков
{
    if (a->size != b->size) {
        return false;
    }
    int i = 0;
    while (i < a->size) {
        if (a->key != b->key) {
	        return false;
        }
        a = a->next;
        b = b->next;
        i++;
  }
  return true;
}

```

#### __пояснение__
+ вычисляем размер двух списков
+ в функции check сразу проверяем размеры списков
+ в цикле while сравниваем списки поэлементно





# __билет 3__ -- реверс дека

#### __Код__

```c
typedef struct Item { // описание структуры узла дека
    int key;
    struct Item *next; // ссылка на след элемент
    struct Item *prev; // ссылка на пред элемент
} Item;

typedef struct deque { // описание структуры дека
    Item *first; // первый элемент дека
    Item *last; // последний элемент дека
    int size;
} deque;

int pop_front(deque *a)
{
    Item temp = a->first;
    int b = temp->key;
    a->first = a->first->next;
    a->size--;
    free(temp);
    return b;
}

void reverse(deque *a) // функция, выполняющая реверс дек
{
    if (!isEmpty(a)) {
        int x = pop_front(a);
        reverse(a);
        push_back(a, x);
    }
}

```
###### примечание
+ можно решить по-другому: создать второй дек и в него считать исходный дек с конца
+ можно переставлять симметричные относительно центра элементы (их ключи) дека (n/2)

#### __пояснение__
+ _функции_
  + ```isEmpty(a)``` -- проверяет на пустоту  
  + ```int pop_front``` -- возвращает первый элемент и удаеляет его
  + ```void push_back``` -- вставляет элемент в конец
  + reverse: сначала создается стек вызовов функции ```pop_front```, после того, как все элеменеты будут удалены, элементы в обратном порядке заполнят дек с помощью функции ```push_back```






# __билет 4__ -- поиск глубины дерева общего вида на си

#### __Код__

```c
typedef struct node { //описание структуры дерева
    int key;
    struct node *son;
    struct node *brother;
} tree;

void depth(tree *root, int *h, int count) //функция определения глубины дерева
{
    if (root != NULL) {
        if (count > *h) *h = count;
        depth(root->son, h, count + 1);
        depth(root->brother, h, count);
    }
}

int main (void)
{
    ...
    int h = 0;
    depth(kor, &h, 0);
    printf("depth_tree = %d\n", h);
    ...
}
```
#### __пояснение__
+ делаем рекурсивный обход в глубину
    + доходим по сыновьям ```root->son``` до ```root->son == NULL``` -- ```depth(root->son, h, count + 1);```
    + доходим по братьям ```root->brother``` до ```root->brother == NULL``` --               ```depth(root->brother, h, count);```

![v4p1](https://github.com/Suraba03/SKATbl/blob/main/sem2/zayka/photo/v4n1.jpg)




# __билет 5__ -- нахождение одинаковых элементов бинарного дерева на си

#### __Код 1__

```c
typedef struct node { // структура бинарного дерева
    int key;
    struct node *left;
    struct node *right;
} tree;

void same(tree *root, int k) // поиск одинаковых элементов
{
    if (root == NULL) return;
    if (root->key == k) {
        printf("Repeat found: %d\n", root->key);
    }
    same(root->left, k);
    same(root->right, k);
}
```

#### __пояснение__
+ обходим дерево в глубину, если ```root->key == k``` выводим ```k```

#### __Код 2__ (родной) так чисто, на всякий случай

```c
typedef struct _vector vector;
struct _vector
{
    int size;
    int *data;
    int count_elem;
};

void resize(vector *v)
{
    v->size++;
    v->data = realloc(v->data, sizeof(int) * v->size);
}

void push_back(vector *v, int value)
{
    if (v->size == v->count_elem) {
        resize(v);
    }
    v->count_elem++;
    v->data[v->count_elem - 1] = value;
}

int *inorder(tree *root, vecrot *v)
{
    if (root != NULL) { // checking if the root is not null
        inorder(root->left); // visiting left child
        push_back(v, root->value);
        inorder(root->right); // visiting right child
    }
}
// здесь функция для вывода повторяющихся элементов отсортированного вектора
```
#### __пояснение__
+ тут нечего пояснять








# __билет 6__ -- реверс файла на си

###### примечание
На вход программе поступает файл, реверс происходит внутри файла

#### __Код__

```c
int main (int argc, char *argv[]) {
    if (argc != 2) return 1;
    FILE *in = fopen(argv[1], "r+");
    if (in == NULL) {
        printf ("file is empty!\n");
        return 1;
    }
    fseek (in, 0, SEEK_END);
    long len = ftell(in); // присваивание размера (кол-ва эл-ов) файла переменной len
    for (long i = 0; i < len / 2; i++) {
        int left, right;
        fseek (in, i, SEEK_SET);
        left = fgetc (in);
        fseek (in, -(i + 1), SEEK_END); // почему же здесь не -i, а потому что здесь будет
                                        // храниться какойто random shiiiiiiit nigga
        right = fgetc (in);
        fseek (in, i, SEEK_SET);
        fputc (right, in); // вставляем в левый элемент то, что сохранили в right
        fseek (in, -(i + 1), SEEK_END);
        fputc (left, in); // вставляем в правый элемент то, что сохранили в left
    }
    fclose (in);
    printf ("check out %s\n", argv[1]);
}
```
###### сслыки
+ [fseek](http://cppstudio.com/post/1628/)
+ [ftell](http://cppstudio.com/post/1618/)
+ [fopen](http://cppstudio.com/post/1253/)
+ [fgetc](http://cppstudio.com/post/1704/)

#### __пояснение__
+ меняем элементы, симметричные относительно центра
+ для понимания функций с файлами можно потыкать ссылки сверху












# __билет 7__ -- сортировка стека

#### __Код 1__ сортировка слиянием

```c
void reverse(stack *a) // функция реверса стека
{
    stack *b;
    create(&b);
    while (!isEmpty(a))
        push(b, pop(a));
    copy(b, a);
}

stack *merge(stack *a, stack *b) // функция слияния двух стеков
{
    stack *res;
    create(&res);
    while (!isEmpty(a) && !isEmpty(b)) {
        if (top(a) < top(b))
	        push(res, pop(a));
        else
	        push(res, pop(b));
    }
    while (!isEmpty(a)) push(res, pop(a));
    while (!isEmpty(b)) push(res, pop(b));
    reverse(res);
    return res;
}

void merge_sort(stack **x)
{
    if (size(*x) > 1) {
        int l = size(*x) / 2;
        stack *a, *b;
        create(&a);
        create(&b);
        for (int i = 0; i < l; i++) push(a, pop (*x)); // заполняем стэк a
        while (!isEmpty(*x)) push(b, pop (*x)); // заполняем стэк b
        merge_sort(&a);
        merge_sort(&b);
        *x = merge(a, b);
    }
}

```
#### __пояснение__

+ функции
    + reverse
        + получает на вход указатель стэк ```a```
        + создает стэк ```b```
        + туда записвает эелементы из ```a``` -- ```push(res, pop(a))```, пока кол-во элментов стэка ```a != 0```
        + Потом копирует стэк ```b``` в стэк ```a```.
    + merge
        + получает на вход указатели на два стэка ```a``` и ```b```.
        + Создает новый стэк ```res```.
        + пока в стэках ```a``` и ```b``` есть элементы: будет выбираться наименьший из элементов, стоящих в начале этих стэков, и записываться в стэк ```res```.
        + после того как один из стэков (```a``` и ```b```) будет пуст, перерепишем все элементы из непустого стэка в ```res``` при помощи ```push(res, pop(a))``` или ```push(res, pop(b))```
        + сделаем реверс стэка ```res``` ```reverse(res)```
        + таким образом получится отсортированный стэк ```res```
    +  merge_sort
        + получает на вход двойной указатель на стэк (чтобы можно было в него что-то сохранять)
        + рекурсия
            + шаг - деление стэка на два, первый стэк будет иметь длину изначального стэка(```l```) ```l / 2```, второй имеет длину размером ```l - l / 2```
            + база - длина стэка, поданного в функцию будет = 1
        + когда пойдут обратные вызовы рекурсии, начнет выполняться функция ```merge(a, b)```.
            + картиночка !!!!
            
	    ![v7n1](https://github.com/Suraba03/SKATbl/blob/main/sem2/zayka/photo/v7n1.png)

+ в ```х``` будет храниться отсортированный стэк


#### __Код 2__ сортировка чем-то еще

```c

```
#### __пояснение__








# __билет 8__ -- транспонирование матрицы из файла

#### __Код__

```c
#include <stdio.h>
#define STR 10
#define SIZE 10

int num_lines(FILE *f)
{
    char c;
    int cnt = 0;
    while ((c = getc(f)) != EOF) {
        if (c == '\n') {
            cnt++;
        }
    }
    cnt++;
    rewind(f);
    return cnt;
}

int num_el(FILE *f)
{
    char c;
    int cnt = 0;
    int flag = 0;
    while ((c = getc(f)) != EOF) { // 48..57
        if (c != '\n' && c != ' ' && c != '\t') {
            if (flag == 0) {
                cnt++;
                flag = 1;
            }
        } else {
            flag = 0;
        }
    }
    rewind(f);
    return cnt;
}

int main(int argc, char *argv[])
{
    char name[STR];
    int mat[SIZE][SIZE];
    scanf("%s", name);
    FILE *f;
    if ((f = fopen(name, "r")) == NULL) {
        printf("файла не существует!\n");
    }
    int n = num_lines(f);
    int m = num_el(f) / num_lines(f);
    for (int i = 0; i < n; i++) { // здесь считываем матрицу
        for (int j = 0; j < m; j++) {
            fscanf(f, "%d", &mat[j][i]);
        }
    }
    for (int i = 0; i < m; i++) { // здесь выводим в транспонированном виде
        for (int j = 0; j < n; j++) {
            printf("%d ", mat[i][j]); // поменяли i и j местами
        }
        printf("\n");
    }
    fclose(f);
    return 0;
}
```
#### __пояснение__
+ функции
    + ```int num_lines(FILE *f)``` -- возвращает кол-во строк
    + ```int num_el(FILE *f)``` -- возвращает кол-во элементов
+ на ввод подается матрица без количества столбцов и строк






# __билет 9__ -- подсчет кол-ва различных элементов дерева

#### __Код__

```c
typedef struct node {
    int key;
    struct node *left;
    struct node *right;
} tree;

void same (tree *root, int k, int *h)
{
    if (root == NULL) return;
    if (root->key != k) *h = *h + 1;
    same (root->left, k);
    same (root->right, k);
}

int main()
{
    ...
    int h;
    if (root != NULL) {
        k = root->key;
    }
    same(root, k, &h)
    printf("%d\n", h);
    ...
}
```
#### __пояснение__

#### __Код 2__ (родной) так чисто, на всякий случай

```c
typedef struct _vector vector;
struct _vector
{
    int size;
    int *data;
    int count_elem;
};

void resize(vector *v)
{
    v->size++;
    v->data = realloc(v->data, sizeof(int) * v->size);
}

void push_back(vector *v, int value)
{
    if (v->size == v->count_elem) {
        resize(v);
    }
    v->count_elem++;
    v->data[v->count_elem - 1] = value;
}

int *inorder(tree *root, vecrot *v)
{
    if (root != NULL) { // checking if the root is not null
        inorder(root->left); // visiting left child
        push_back(v, root->value);
        inorder(root->right); // visiting right child
    }
}
// здесь функция для вывода неповторяющихся элементов отсортированного вектора
```

#### __пояснение__





# __билет 10__ -- удаление листьев (удаление узла двоичного дерева ???)

#### __Код__ -- удаление листьев

```c
struct node {
    struct node *left;
    struct node *right;
    int value;
}

typedef struct Tree {
    struct node *root;
} tree;

typedef struct vector {
    int number_of_elements;
    int capacity;
    node *number;
} vector;

void search_leafs(tree **root, vector node *(*leafs))
{
    int result;
    if (((*root)->left == NULL) && ((*root)->right == NULL)) {
        push_back(leafs, (*root));
    }
    if ((*root)->left) search_leafs((*root)->left);
    if ((*root)->right) search_leafs((*root)->right);
}

void delete_list(vector node *(*leafs))
{
    for (int i = 0; i < leafs->number_of_elements; i++) {
        free(leafs->number[i]);
    }
}
```
#### __пояснение__
+ запишем в дин. массив указателей на структуру ```tree``` листья дерева, обойдя его в глубину
+ удалим по указателям элементы вектора, тем самым удалив листья дерева







# __билет 11__ -- конкатенация трех файлов на си

#### __Код__

```c
int main ()
{
    unsigned char ch; // Так как бинарный режим чтения
                      //файлов, то нужен диапозон значений 0 - 255
    FILE *f1 = fopen ("f1.bin", "rb");
    FILE *f2 = fopen ("f2.bin", "rb");
    FILE *f3 = fopen ("f3.bin", "rb");
    FILE *f = fopen ("f.bin", "wb");
    while (fread(&ch, 1, 1, f1)
        fwrite(&ch, 1, 1, f);
    while (fread(&ch, 1, 1, f2))
        fwrite(&ch, 1, 1, f);
    while (fread(&ch, 1, 1, f3))
        fwrite(&ch, 1, 1, f);
    fclose(f1); fclose(f2); fclose(f3); fclose(f);
    return 0;
} // вариант с бинарным файлом

int main(void)
{
    FILE *f1 = fopen ("f1.txt", "r");
    FILE *f2 = fopen ("f2.txt", "r");
    FILE *f3 = fopen ("f3.txt", "r");
    FILE *f = fopen ("f.txt", "w");
    char c;
    while ((c = getc (f1)) != EOF)
        putc (c, f);
    while ((c = getc (f2)) != EOF)
        putc (c, f);
    while ((c = getc (f3)) != EOF)
        putc (c, f);
    fclose (f1); fclose (f2); fclose (f3); fclose (f);
    return 0;
}
```
#### __пояснение__
+ считываем и записываем поэлементно каждый символ из файлов f1, f2, f3 в f








# __билет 12__ -- нерекурсивная сортировка Хоара на си

#### __Код__

```c
void Quick (int arr[], int n)
{
    int base, left, right, i, j;
    base = left = right = i = j = 0;
    stack *st;
    push (st, n - 1);
    push (st, 0);
    do {
        left = Pop (st);
        right = Pop (st);
        if (((right - left) == 1) && (arr[left] > arr[right])) {
	        swap (arr[left], arr[right]);
        } else {
            base = arr[(left + right) / 2];
        	i = left;
        	j = right;
        	do {
        	    while ((base > arr[i])) ++i;
        	    while (arr[j] > base) --j;
        	    if (i <= j) swap(arr[i++], arr[j--]);
            } while (i <= j);
	    }
        if (left < j) {
	        push (st, j);
	        push (st, left);
	    }
        if (i < right) {
	        push (st, right);
	        push (st, i);
	    }
    } while (top (st) != NULL);
}
```
#### __пояснение__ -- еще не готово










# __билет 13__ -- вычислить константное булевское выражение с помощью обратной польской записи

#### __Код__

```c
typedef enum {
    FINAL, // Идентификатор конца входной строки
    OPERAND,
    OPERATOR,
    BRACKET
} TokenType;

typedef struct {
    TokenType type;
    union {
        char operand; // 0 или 1
        char operator_name;
        bool is_left_bracket; // Левая скобка - истина, правая - ложь
    } data;
} Token; // Именно они будут в узлах дерева выражений
```
#### __пояснение__

+ реализовать функцию ввода токенов, что она делает
    + если встретит разделительные символы, то при помощи цикла while, пропустит их
    + если встретит 1, 0, |, &, то запишет в массив токенов только что введенный символ
    + если встретит (, ), то запишет в массив токенов True, если была введена (, иначе - False
    + если встретит конец файла, то закончится считываение токенов (```t->type = FINAL```)
+ создадим бинарное дерево, заполним его данными из массива токенов по правилам
    + в корне будет находиться оператор с самым меньшим приоритетом, т.е. последний в строке символ - '|', пример ((1 & 0) | 1) х|х ((0 & 1)
    + и тд
+ сделать обратный обход бинарного дерева, записать его значения в новый массив токенов

![v13n1](https://github.com/Suraba03/SKATbl/blob/main/sem2/zayka/photo/v13n1.png)

+ обратная польская нотация

![v13n2](https://github.com/Suraba03/SKATbl/blob/main/sem2/zayka/photo/v13n2.png)

+ до обхода дерева: [1, &, 0, |, 1, |, 0, &, 1], после: постфиксная нотация [1, 0, &, 1, |, 0, 1, &, |]
+ обходим массив, при встрече тройки токенов вида операнд,операнд,операция, делаем следующую замену
    + 00| -> 0, иначе ??| -> 1
    + 11& -> 0, иначе ??& -> 0
    + повторяем эти действия, пока не останется один операнд, это и будет ответ







# __билет 14__ -- проверка вложенности скобок

#### __Код__

```c
#include <stdio.h>
#include <string.h>
#define STR_LEN 50

int check(char *str)
{
    int cnt = 0;
    for (int i = 0; i < strlen(str); i++) {
        if (str[i] == '(') {
            cnt++;
        } else {
            cnt--;
        }
        if (cnt < 0) {
            return 0;
        }
    }
    return (cnt == 0);
}

int main()
{
    char str[STR_LEN];
    scanf("%s", str);
    printf("%s", check(str) ? "TRUE\n" : "FALSE\n");
}
```
#### __пояснение__
+ идем циклом for по строке, если видим "(", то увеличиваем счетчик на один, иначе уменьшаем
+ после каждого изменения счетчика, нужно проыерить его на отрицательность, если True, то вернуть ноль
- то же самое можно реализовать на стэке
    - открывающиеся скобки добаялем в стэк, если встречается закрывающаяся, то выталкиваем элемент из стэка
    - если стэк перед выталкиванием оказался пуст => возвращаем False
    - при удачном считывании последовательности
        - если стэк оказался пуст, то возвращаем True
        - иначе False






# __билет 15__ -- вычислить выражение в обратной польской нотации, состоящее из целых чисел

#### __Код__

```c
typedef union _data data;
union {
    int *value_int;
    char *value_char;
} _data;

typedef struct list {
    int number_of_elements;
    int capacity;
    data *arr;
} list;
```
#### __пояснение__
+ реализуем структуру списка списка, куда будем записывать наше выражение. будет три поля
    + кол-во элементов
    + вместимость
    + массив структур объедиенения (```union```) типов ```int```, ```char```
+ будем считывать посимвольно
...
+ мы считали токены куда-то
+ расматриваем тройки токенов слева направо. выполняем следующие замены
    + ab+ = a + b
    + ab* = a * b
    + ab- = a - b
    + ab/ = a / b
+ выполняем эти замены пока в структуре не останется одно число, которое и будет ответом.




После этот переведем строку в ```int``` с помощью функции ```atoi(str)```


# __билет 16__ -- удаление *1 или +0 из дерева

#### __Код__

```c
if (root->left != NULL && root->left->left != NULL && root->left->right != NULL)
  task (root->left);
if (root->right != NULL && root->right->left != NULL && root->right->right != NULL)
  task (root->right);
if ((root->key == '*') && ((root->left->key == '1') || (root->right->key == '1'))) {
    if (root->left->key == '1') {
        free (root->left);
        tmp = root->right;
        free (root);
        root = tmp;
    }
    if (root->right->key == '1') {
        free (root->right);
        tmp = root->left;
        free (root);
        root = tmp;
    }
}
```
#### __пояснение__
+ рекурсивными вызовами "спускаемся" к узлу с двумя сыновьями, чтобы у узла было два операнда
+ если в узле лежит "*" и либо справа, либо слева лежит "1", то
    + если "1" находится слева, то удаляем узел с "1", удаляем узел с "*", на его место ставим правый операнд
    + если "1" находится справа, то удаляем узел с "1", удаляем узел с "*", на его место ставим левый операнд
+ аналогично с +0, "+" ~ "*", "0" ~ "1"
