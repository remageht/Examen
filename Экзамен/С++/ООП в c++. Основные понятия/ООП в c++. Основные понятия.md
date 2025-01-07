### Объявление класса (Class Declaration)

#### Разница между struct и class (Difference between struct and class)

- **struct**:
    
    - По умолчанию все члены `struct` имеют публичный доступ.
        
    - Используется для объединения данных без методов.
        
    - Пример:
        
        
        ```cpp
        struct MyStruct {
            int x;
            int y;
        };
        ```
        
- **class**:
    
    - По умолчанию все члены `class` имеют приватный доступ.
        
    - Используется для объединения данных и методов, реализующих логику.
        
    - Пример:

        
        ```cpp
        class MyClass {
        private:
            int x;
            int y;
        public:
            void setValues(int a, int b) {
                x = a;
                y = b;
            }
            void display() {
                std::cout << "x: " << x << ", y: " << y << std::endl;
            }
        };
        ```
        

#### Вложенные классы (Nested Classes)

- **Описание**: Классы могут быть вложены в другие классы, что позволяет организовывать код и ограничивать доступ.
    
- **Пример**:
    
    
    ```cpp
    class OuterClass {
    public:
        class InnerClass {
        public:
            void display() {
                std::cout << "Inner Class" << std::endl;
            }
        };
    };
    ```
    

### Поля (Fields)

#### Поля объекта (Object fields)

- **Обычные (Regular)**:
    
    - **Объявление (Declaration)**: Обычные поля объявляются как переменные-члены класса.

        
        ```cpp
        class MyClass {
        public:
            int myField;
        };
        ```
        
    - **Инициализация (Initialization)**: Инициализация полей может быть выполнена в конструкторе класса.

        
        ```cpp
        MyClass() : myField(10) {}
        ```
        
    - **Доступ (Access)**: Доступ к полям осуществляется через объект класса.

        
        ```cpp
        MyClass obj;
        std::cout << obj.myField;
        ```
        
- **Константные (Constant)**:
    
    - Описание: Константные поля не могут быть изменены после инициализации.
        
    - Пример:


        ```cpp
        class MyClass {
        public:
            const int myConstField;
            MyClass(int value) : myConstField(value) {}
        };
        ```
        
- **Указатели (Pointers)**:
    
    - Описание: Указатели на поля могут хранить адреса других переменных.
        
    - Пример:

        
        ```cpp
        class MyClass {
        public:
            int* ptr;
            MyClass(int* p) : ptr(p) {}
        };
        ```
        
- **Ссылки (References)**:
    
    - Описание: Ссылки на поля связывают поля с другими переменными.
        
    - Пример:

        
        ```cpp
        class MyClass {
        public:
            int& ref;
            MyClass(int& r) : ref(r) {}
        };
        ```
        
- **mutable**:
    
    - Назначение: Позволяет изменять члены объекта, объявленные как const.
        
    - Пример:
        

		```cpp
        class MyClass {
        public:
            mutable int mutableField;
            MyClass() : mutableField(0) {}
            void setValue(int value) const {
                mutableField = value;
            }
        };
        ```
        

#### Поля класса (Class fields - static fields)

- **Обычные (Regular)**:
    
    - **Объявление (Declaration)**: Статические поля объявляются с ключевым словом `static`.

        
        ```cpp
        class MyClass {
        public:
            static int staticField;
        };
        int MyClass::staticField = 0; // Определение вне класса
        ```
        
    - **Инициализация (Initialization)**: Инициализация статических полей выполняется вне класса.

        
        ```cpp
        int MyClass::staticField = 10;
        ```
        
    - **Доступ (Access)**: Доступ к статическим полям осуществляется через имя класса.

        
        ```cpp
        std::cout << MyClass::staticField;
        ```
        
- **Константные (Constant)**:
    
    - Описание: Константные статические поля не могут быть изменены после инициализации.
        
    - Пример:

        
        ```cpp
        class MyClass {
        public:
            static const int constStaticField;
        };
        const int MyClass::constStaticField = 100;
        ```
        
- **Указатели (Pointers)**:
    
    - Описание: Указатели на статические поля могут хранить адреса других переменных.
        
    - Пример:

        
        ```cpp
        class MyClass {
        public:
            static int* staticPtr;
        };
        int* MyClass::staticPtr = nullptr;
        ```
        
- **Ссылки (References)**:
    
    - Описание: Ссылки на статические поля связывают поля с другими переменными.
        
    - Пример:

        
        ```cpp
        class MyClass {
        public:
            static int& staticRef;
        };
        int globalVar = 100
        int& MyClass::staticRef = globalVar;
        ```
    
    
### Методы (Methods)

#### **Способы определения метода (Ways to define a method)**

1. **В теле класса (In the class body)**
    
    - **Описание**: Методы могут быть определены непосредственно внутри тела класса.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            void display() {
                std::cout << "Hello from MyClass!" << std::endl;
            }
        };
        ```
        
2. **Вне тела класса (Outside the class body)**
    
    - **Описание**: Методы могут быть объявлены в классе и определены вне его тела.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            void display();
        };
        
        void MyClass::display() {
            std::cout << "Hello from MyClass!" << std::endl;
        }
        ```
        

#### **Методы объекта (Object methods - non-static methods)**

1. **Обычные (Regular)**
    
    - **Описание**: Методы, которые могут быть вызваны только объектом класса.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            void display() {
                std::cout << "Hello from MyClass!" << std::endl;
            }
        };
        MyClass obj;
        obj.display(); // Вызов обычного метода
        ```
        
2. **Константные и не константные версии одного метода (Constant and non-constant versions of the same method)**
    
    - **Описание**: Константные методы не могут изменять состояние объекта.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            void display() const {
                std::cout << "Hello from const MyClass!" << std::endl;
            }
            void display() {
                std::cout << "Hello from non-const MyClass!" << std::endl;
            }
        };
        const MyClass constObj;
        MyClass obj;
        constObj.display(); // Вызов константной версии
        obj.display(); // Вызов не константной версии
        ```
        
3. **Виртуальные (Virtual)**
    
    - **Описание**: Методы, которые могут быть переопределены в производных классах для реализации полиморфизма.
        
    - **Пример**:
        
        ```cpp
        class Base {
        public:
            virtual void display() {
                std::cout << "Hello from Base!" << std::endl;
            }
        };
        
        class Derived : public Base {
        public:
            void display() override {
                std::cout << "Hello from Derived!" << std::endl;
            }
        };
        Base* basePtr = new Derived();
        basePtr->display(); // Вызов виртуального метода
        ```
        
4. **Чистые виртуальные (абстрактные) (Pure virtual (abstract))**
    
    - **Описание**: Методы, которые должны быть реализованы в производных классах.
        
    - **Пример**:
        
        ```cpp
        class Abstract {
        public:
            virtual void pureVirtualMethod() = 0; // Чистый виртуальный метод
        };
        
        class Concrete : public Abstract {
        public:
            void pureVirtualMethod() override {
                std::cout << "Implementation in Concrete!" << std::endl;
            }
        };
        Concrete obj;
        obj.pureVirtualMethod(); // Вызов чистого виртуального метода
        ```
        

#### **Методы класса (Class methods - static methods)**

1. **Объявление (Declaration)**
    
    - **Описание**: Статические методы объявляются с ключевым словом `static`.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            static void staticMethod();
        };
        ```
        
2. **Определение (Definition)**
    
    - **Описание**: Статические методы определяются вне класса.
        
    - **Пример**:
        
        ```cpp
        void MyClass::staticMethod() {
            std::cout << "Hello from static method!" << std::endl;
        }
        ```
        
3. **Использование (Usage)**
    
    - **Описание**: Статические методы вызываются без создания объекта класса.
        
    - **Пример**:
        
        ```cpp
        MyClass::staticMethod();
        ```
        

#### **Невянный параметр this и const this (Implicit parameter this and const this)**

- **Описание**: Все методы объекта имеют неявный указатель `this`, который указывает на текущий объект. Константные методы имеют `const this`.
    
- **Пример**:
    
    ```cpp
    class MyClass {
    public:
        void display() const {
            std::cout << "Address of current object: " << this << std::endl;
        }
    };
    MyClass obj;
    obj.display();
    ```
    

#### **Ключевые слова (Keywords)**

1. **default**
    
    - **Описание**: Используется для указания компилятору автоматически сгенерировать реализацию метода по умолчанию.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            MyClass() = default; // Конструктор по умолчанию
        };
        ```
        
2. **delete**
    
    - **Описание**: Используется для удаления функций, предотвращая их использование.
        
    - **Пример**:
        
        ```cpp
        class MyClass {
        public:
            MyClass(const MyClass&) = delete; // Запрещает копирование
        };
        ```
        
3. **final**
    
    - **Описание**: Используется для предотвращения переопределения метода в производных классах.
        
    - **Пример**:
        
        ```cpp
        class Base {
        public:
            virtual void display() final {
                std::cout << "Base display" << std::endl;
            }
        };
        
        class Derived : public Base {
        public:
            // void display() override; // Ошибка, так как метод final
        };
        ```
        

### Квалификаторы доступа (Access Specifiers)

- **public**: Доступны всем.
    
    ```cpp
    public:
        int publicVar;
    ```
    
- **private**: Доступны только членам класса.
    
    ```cpp
    private:
        int privateVar;
    ```
    
- **protected**: Доступны членам класса и производным классам.
    
    ```cpp
    protected:
        int protectedVar;
    ```
    
- **ключевое слово friend (friend keyword)**: Позволяет дружественным функциям и классам доступ к приватным и защищенным членам.
    
    ```cpp
    class MyClass {
        friend void friendFunction(MyClass&);
        friend class FriendClass;
    };
    
    void friendFunction(MyClass& obj) {
        // Доступ к приватным членам obj
    }
    ```
    

### Устройство объекта в памяти (Object Layout in Memory)

#### **Занимают ли методы место в памяти объекта (Do methods occupy space in the object's memory)**

- **Описание**: Методы не занимают место в памяти объекта; они выделяются отдельно как функции. Только данные-члены объекта занимают память.
    

#### **Размер объекта (Object Size)**

1. **Без виртуальных функций (Without virtual functions)**
    
    - Описание: Размер объекта определяется размером его данных-членов.
        
    - Пример:
        
        ```cpp
        class MyClass {
        public:
            int a;
            double b;
        };
        ```
        
2. **С виртуальными функциями (With virtual functions)**
    
    - Описание: Объект с виртуальными функциями содержит указатель на таблицу виртуальных функций (vtable).
        
    - Пример:
        
        ```cpp
        class MyClass {
        public:
            virtual void myMethod();
            int a;
        };
        ```