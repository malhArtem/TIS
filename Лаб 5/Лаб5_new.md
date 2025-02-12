# Использование Google Test

### 1. Создание проекта Google Test в Visual Studio

1. Откройте Visual Studio.
2. Перейдите в меню File -> New -> Project.
3. В окне создания проекта выберите Google Test (этот шаблон доступен, если у вас установлена поддержка C++ и тестирования в Visual Studio).
   - Если шаблона Google Test нет, убедитесь, что у вас установлен компонент "Desktop Development with C++" и "Testing tools core features" в Visual Studio Installer.
4. Назовите проект, например, MyGoogleTests, и нажмите Create.

---

### 2. Структура проекта Google Test

После создания проекта вы увидите следующую структуру:
- **pch.h**: Precompiled header (может быть отключен, если не используется).
- **test.cpp**: Пример тестового файла, где вы будете писать свои тесты.

Visual Studio автоматически настраивает проект для использования Google Test, включая пути к библиотекам и заголовочным файлам.

---

### 3. Написание тестов

Теперь вы можете писать тесты в файле MyGoogleTests.cpp или создать новый файл для тестов. Рассмотрим пример:

#### Пример тестового файла
```
#include "pch.h"  // Подключение precompiled header (если используется)
#include <gtest/gtest.h>

// Пример функции для тестирования
int Multiply(int a, int b) {
    return a * b;
}

// Тестовый случай для функции Multiply
TEST(MultiplyTest, HandlesPositiveInput) {
    EXPECT_EQ(Multiply(2, 3), 6);
    EXPECT_EQ(Multiply(5, 10), 50);
}

TEST(MultiplyTest, HandlesZeroInput) {
    EXPECT_EQ(Multiply(0, 5), 0);
    EXPECT_EQ(Multiply(10, 0), 0);
}

TEST(MultiplyTest, HandlesNegativeInput) {
    EXPECT_EQ(Multiply(-2, 3), -6);
    EXPECT_EQ(Multiply(-4, -5), 20);
}
```
---

### 4. ЗапускСоберите проектите проектBuild -> Build Solutiond Solution** (или Ctrl + Shift + B).
2. **Запустите тесты**:
   - ПTest -> Run All Tests Run All Tests** (или используйте сочетание клавиш Ctrl + R, A).
   Test Explorer*TTest -> Windows -> Test Explorer Test Explorer**) и запустите тесты оттуда.

---

### 5. Использование Test Explorer

Test Explorer — это удобный инструмент для управления тестами в Visual StudTest Explorer*TTest -> Windows -> Test Explorer Test Explorer**).
2. Здесь вы увидите список всех тестов, их статус (Passed/Failed) и время выполнения.
3. Вы можете запускать отдельные тесты, группировать их по категориям и анализировать результаты.

---

### 6. Добавление новых тестовых файлов

Если вы хотите добавить новый файл для тестов:
1. Щелкните правой кнопкой мыши на проект в Solution ExplorAdd -> New Itemdd -> New ItemC++ Fileите **C++ File** и назовите его, например, MoreTests.cpp.
4. Напишите тесты в этом файле, не забывая подключить #include <gtest/gtest.h>.

Пример нового файла:

```
#include "pch.h"
#include <gtest/gtest.h>

TEST(MoreTests, SimpleTest) {
    EXPECT_TRUE(1 + 1 == 2);
}
```
---

### 7. Настройка проекта (опционально)

Если вам нужно настроить проект вручную (например, добавить дополнительные библиотеки или изменить параметры сборки):
1. Щелкните правой кнопкой мыши на прPropertiesе **Properties*C/C++ -> GeneralC++ -> General** вы можете добавить дополнительные include-директориLinker -> Inputinker -> Input** вы можете добавить дополнительные библиотеки.

---

### 8. Пример использования фикстур (Fixtures)

Google Test поддерживает фикстуры для создания общих настроек для группы тестов. Пример:
``` cpp
#include "pch.h"
#include <gtest/gtest.h>

// Фикстура для тестов
class MyFixture : public ::testing::Test {
protected:
    void SetUp() override {
        // Код, который выполняется перед каждым тестом
        value = 42;
    }
void TearDown() override {
        // Код, который выполняется после каждого теста
    }

    int value;
};

// Использование фикстуры
TEST_F(MyFixture, TestWithFixture) {
    EXPECT_EQ(value, 42);
    value += 1;
    EXPECT_EQ(value, 43);
}
```

---

