### Глобальные переменные и функции

При использовании с глобальными переменными и функциями, `static` ограничивает область их видимости файлом, в котором они объявлены, предотвращая использование этих переменных и функций в других файлах.
```
// file1.cpp
static int globalVar = 10;

static void myFunction() {
    std::cout << "Hello from file1!" << std::endl;
}

// file2.cpp
extern int globalVar; // Ошибка: globalVar недоступен
extern void myFunction(); // Ошибка: myFunction недоступна

```