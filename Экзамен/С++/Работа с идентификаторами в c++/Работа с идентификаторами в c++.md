### **1. Допустимые идентификаторы в C++**

#### **Идентификаторы переменных**

- **Описание**: Идентификаторы переменных используются для наименования переменных. Они должны начинаться с буквы или символа подчеркивания (_), за которыми могут следовать буквы, цифры или подчеркивания.
    
- **Примеры**:
    
    ```cpp
    int myVariable;
    double _value;
    char character_1;
    ```
    

#### **Идентификаторы функций**

- **Описание**: Идентификаторы функций используются для наименования функций. Правила те же, что и для имен переменных.
    
- **Примеры**:

    
    ```cpp
    void myFunction() {
        // код функции
    }
    
    int addNumbers(int a, int b) {
        return a + b;
    }
    ```
    

#### **Идентификаторы макросов**

- **Описание**: Идентификаторы макросов используются для определения макросов препроцессора, которые расширяют возможности кода.
    
- **Примеры**:

    
    ```cpp
    #define PI 3.14159
    #define MAX(a, b) ((a) > (b) ? (a) : (b))
    
    int main() {
        double radius = 5.0;
        double area = PI * radius * radius;
        int maxValue = MAX(10, 20);
    }
    ```
    

### **2. Пространства имён (Namespaces)**

#### **std**

- **Описание**: Пространство имён `std` содержит большинство стандартных функций и классов, включая потоки ввода-вывода, контейнеры и алгоритмы.
    
- **Пример**:

    
    ```cpp
    #include <iostream>
    #include <vector>
    
    int main() {
        std::cout << "Hello, world!" << std::endl;
    
        std::vector<int> myVector = {1, 2, 3, 4, 5};
        for (int num : myVector) {
            std::cout << num << " ";
        }
    }
    ```
    

#### **Анонимные пространства имён**

- **Описание**: Анонимные пространства имён используются для ограничения видимости функций и переменных внутри одного файла, предотвращая конфликты имен между файлами.
    
- **Пример**:
    
    
    ```cpp
    namespace {
        int secretVar = 42;
    
        void displaySecret() {
            std::cout << "Secret: " << secretVar << std::endl;
        }
    }
    
    int main() {
        displaySecret(); // Выводит: Secret: 42
    }
    ```
    

#### **Именованные пространства имён**

- **Описание**: Именованные пространства имён используются для организации кода и предотвращения конфликтов имен.
    
- **Пример**:
 
    
    ```cpp
    namespace MyNamespace {
        int myVar = 10;
    
        void displayVar() {
            std::cout << "myVar: " << myVar << std::endl;
        }
    }
    
    int main() {
        MyNamespace::displayVar(); // Выводит: myVar: 10
    }
    ```
    

#### **Встроенные пространства имён**

- **Описание**: Встроенные пространства имён используются для определения новых пространств имён внутри существующих, позволяя более гибко организовывать код.
    
- **Пример**:

    
    ```cpp
    namespace Outer {
        int outerVar = 100;
    
        namespace Inner {
            int innerVar = 200;
    
            void displayVars() {
                std::cout << "outerVar: " << outerVar << std::endl;
                std::cout << "innerVar: " << innerVar << std::endl;
            }
        }
    }
    
    int main() {
        Outer::Inner::displayVars();
        // Выводит:
        // outerVar: 100
        // innerVar: 200
    }
    ```
    

#### **using**

- **Описание**: Ключевое слово `using` используется для упрощения доступа к членам пространства имён, позволяя избежать необходимости указывать полное имя пространства имён.
    
- **Пример**:

    
    ```cpp
    #include <iostream>
    using std::cout;
    using std::endl;
    
    int main() {
        cout << "Hello, world!" << endl;
    }
    ```
    

#### **using namespace**

- **Описание**: Директива `using namespace` позволяет использовать все члены указанного пространства имён, делая код короче.
    
- **Пример**:

    
    ```cpp
    #include <iostream>
    using namespace std;
    
    int main() {
        cout << "Hello, world!" << endl;
    }
    ```

### 1. Области видимости (Scope)

#### **Сокрытие (Shadowing)**

- **Описание**: Сокрытие происходит, когда локальная переменная или функция имеет то же имя, что и глобальная переменная или функция, тем самым скрывая глобальную переменную или функцию в своей области видимости.
    
- **Примеры**:

    
    ```cpp
    int x = 5; // Глобальная переменная
    
    void exampleFunction() {
        int x = 10; // Локальная переменная скрывает глобальную переменную x
        std::cout << x << std::endl; // Выводит: 10
    }
    ```
    
- **Сокрытие переменных (Variables)**: Происходит, когда локальная переменная в функции или блоке скрывает глобальную переменную с тем же именем.
    
    - **Пример**:
    
        
        ```cpp
        int globalVar = 1;
        
        void func() {
            int globalVar = 2; // Локальная переменная скрывает глобальную
            std::cout << globalVar << std::endl; // Выводит: 2
        }
        ```
        
- **Сокрытие функций (Functions)**: Происходит, когда функция, объявленная в блоке кода, имеет то же имя, что и функция глобального уровня или уровня пространства имен.
    
    - **Пример**:
    
        
        ```cpp
        void myFunc() {
            std::cout << "Global myFunc" << std::endl;
        }
        
        void anotherFunc() {
            void myFunc() {
                std::cout << "Local myFunc" << std::endl;
            }
            myFunc(); // Выводит: Local myFunc
        }
        
        int main() {
            anotherFunc();
            myFunc(); // Выводит: Global myFunc
        }
        ```
        
- **Сокрытие типов (Types)**: Происходит, когда локально определенный тип скрывает глобально определенный тип с тем же именем.
    
    - **Пример**:

        
        ```cpp
        typedef int MyType;
        
        void func() {
            typedef float MyType; // Локальное определение скрывает глобальное
            MyType var = 5.5;
            std::cout << var << std::endl; // Выводит: 5.5
        }
        
        int main() {
            MyType var = 5;
            std::cout << var << std::endl; // Выводит: 5
            func();
        }
        ```
        

#### **Глобальные (Global Scope)**

- **Описание**: Глобальная область видимости распространяется на переменные и функции, объявленные вне всех функций и блоков.
    
- **Пример**:

    
    ```cpp
    int globalVar = 42;
    
    void displayGlobalVar() {
        std::cout << globalVar << std::endl; // Выводит: 42
    }
    
    int main() {
        displayGlobalVar();
    }
    ```
    

#### **Локальные (Local Scope)**

- **Описание**: Локальная область видимости распространяется на переменные и функции, объявленные внутри функции или блока кода.
    
- **Пример**:

    
    ```cpp
    void exampleFunction() {
        int localVar = 10;
        std::cout << localVar << std::endl; // Выводит: 10
    }
    ```
    

#### **Связь области видимости идентификатора и времени жизни переменной (Relationship between scope of identifier and variable lifetime)**

- **Описание**: Локальные переменные создаются при входе в блок кода и уничтожаются при выходе из него, в то время как глобальные переменные существуют на протяжении всей работы программы.
    
- **Пример**:

    
    ```cpp
    int globalVar = 42;
    
    void exampleFunction() {
        int localVar = 10; // Локальная переменная
        std::cout << "Local var: " << localVar << std::endl;
    } // localVar уничтожается здесь
    
    int main() {
        exampleFunction();
        std::cout << "Global var: " << globalVar << std::endl; // Выводит: Global var: 42
    }
    ```
    

### 2. Связывание (Binding)

#### **Статическое связывание (Static Binding)**

- **Описание**: Статическое связывание (лексическое связывание) происходит на этапе компиляции. Компилятор определяет, к какой переменной или функции относится идентификатор.
    
- **Пример**:

    
    ```cpp
    int x = 10;
    
    void exampleFunction() {
        int x = 20; // Локальная переменная x
        std::cout << x << std::endl; // Выводит: 20
    }
    
    int main() {
        exampleFunction();
        std::cout << x << std::endl; // Выводит: 10
    }
    ```
    

#### **Динамическое связывание (Dynamic Binding)**

- **Описание**: Динамическое связывание происходит на этапе выполнения программы. Используется для виртуальных функций в полиморфизме.
    
- **Пример**:

    
    ```cpp
    class Base {
    public:
        virtual void show() {
            std::cout << "Base class" << std::endl;
        }
    };
    
    class Derived : public Base {
    public:
        void show() override {
            std::cout << "Derived class" << std::endl;
        }
    };
    
    void display(Base* base) {
        base->show(); // Динамическое связывание
    }
    
    int main() {
        Base base;
        Derived derived;
        display(&base); // Выводит: Base class
        display(&derived); // Выводит: Derived class
    }
    ```
    

#### **Связывание виртуальных функций (Binding of virtual functions)**

- **Описание**: Связывание виртуальных функций используется для полиморфизма, позволяя переопределять методы базового класса в производных классах и вызывать их через указатели базового класса.
    
- **Пример**:

    
    ```cpp
    class Animal {
    public:
        virtual void speak() {
            std::cout << "Animal speaks" << std::endl;
        }
    };
    
    class Dog : public Animal {
    public:
        void speak() override {
            std::cout << "Dog barks" << std::endl;
        }
    };
    
    void makeAnimalSpeak(Animal* animal) {
        animal->speak(); // Связывание виртуальной функции
    }
    
    int main() {
        Animal animal;
        Dog dog;
        makeAnimalSpeak(&animal); // Выводит: Animal speaks
        makeAnimalSpeak(&dog); // Выводит: Dog barks
    }
    ```