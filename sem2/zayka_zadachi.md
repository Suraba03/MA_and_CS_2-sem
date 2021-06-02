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
![v4p1](...)




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

```
#### __пояснение__

#### __Код 2__ сортировка ...

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

#### __Код__

```c

```
#### __пояснение__







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
#### __пояснение__








# __билет 13__ -- поиск глубины дерева общего вида на си

#### __Код__

```c

```
#### __пояснение__







# __билет 14__ -- поиск глубины дерева общего вида на си

#### __Код__

```c

```
#### __пояснение__







# __билет 15__ -- поиск глубины дерева общего вида на си

#### __Код__

```c

```
#### __пояснение__








# __билет 16__ -- поиск глубины дерева общего вида на си

#### __Код__

```c

```
#### __пояснение__
