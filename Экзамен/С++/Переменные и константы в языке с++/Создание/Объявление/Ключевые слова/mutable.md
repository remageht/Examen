Ключевое слово `mutable` в C++ используется для обозначения того, что член класса может изменяться, даже если объект, содержащий его, объявлен как `const`. Это особенно полезно, когда вы хотите изменить внутреннее состояние объекта в методе, который должен оставаться логически `const`.

### Пример использования `mutable`:

Предположим, у вас есть класс с методом, который помечен как `const`, но вам нужно изменять некоторые его члены. В этом случае вы можете использовать `mutable` для таких членов класса.
```
class MyClass {
public:
    MyClass() : counter(0) {}

    void increment() const {
        counter++; // Можно изменять, так как counter помечен как mutable
    }

    int getCounter() const {
        return counter;
    }

private:
    mutable int counter; // Можем изменять, даже если метод const
};

int main() {
    const MyClass obj;
    obj.increment(); // Корректно, несмотря на const
    std::cout << "Counter: " << obj.getCounter() << std::endl;
    return 0;
}

```

В этом примере:

- Класс `MyClass` содержит член `counter`, который помечен как `mutable`.
    
- Метод `increment()` помечен как `const`, но он изменяет значение `counter`, так как `counter` объявлен с использованием `mutable`.
    

