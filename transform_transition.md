# Конспект: CSS-анимация с использованием `transition` и `transform`

## 1. Введение

CSS предоставляет мощные инструменты для создания анимаций без использования JavaScript. Два ключевых свойства — `transition` и `transform` — позволяют создавать плавные визуальные эффекты, улучшающие пользовательский опыт.

---

## 2. Свойство `transition`

### 2.1. Назначение
`transition` обеспечивает плавный переход между двумя состояниями элемента при изменении его CSS-свойств.

### 2.2. Синтаксис
```css
transition: [свойство] [длительность] [функция времени] [задержка];
```

### 2.3. Параметры

| Параметр | Описание | Примеры |
|----------|----------|---------|
| **свойство** | CSS-свойство для анимации | `opacity`, `background-color`, `all` |
| **длительность** | Время перехода | `0.3s`, `500ms` |
| **функция времени** | Кривая скорости анимации | `ease`, `linear`, `ease-in-out` |
| **задержка** | Задержка перед началом | `0s`, `0.2s` |

### 2.4. Примеры

**Базовый пример:**
```css
.button {
  background-color: blue;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: red;
}
```

**Множественные переходы:**
```css
.card {
  transition: 
    transform 0.3s ease,
    opacity 0.5s ease-in-out;
}
```

**Все свойства:**
```css
.element {
  transition: all 0.4s ease;
}
```

### 2.5. Функции времени (timing functions)

- `ease` — медленный старт и финиш (по умолчанию)
- `linear` — равномерная скорость
- `ease-in` — медленный старт
- `ease-out` — медленный финиш
- `ease-in-out` — медленный старт и финиш
- `cubic-bezier(x1, y1, x2, y2)` — пользовательская кривая

---

## 3. Свойство `transform`

### 3.1. Назначение
`transform` позволяет изменять положение, размер и форму элемента в 2D или 3D пространстве.

### 3.2. Основные функции трансформации

#### 2D-трансформации:

| Функция | Описание | Пример |
|---------|----------|--------|
| `translate(x, y)` | Перемещение | `translate(50px, 100px)` |
| `translateX(x)` | Перемещение по X | `translateX(20px)` |
| `translateY(y)` | Перемещение по Y | `translateY(-30px)` |
| `scale(x, y)` | Масштабирование | `scale(1.5, 1.5)` |
| `scaleX(x)` | Масштаб по X | `scaleX(2)` |
| `scaleY(y)` | Масштаб по Y | `scaleY(0.5)` |
| `rotate(angle)` | Поворот | `rotate(45deg)` |
| `skew(x, y)` | Наклон | `skew(10deg, 5deg)` |

#### 3D-трансформации:

| Функция | Описание | Пример |
|---------|----------|--------|
| `translateZ(z)` | Перемещение по Z | `translateZ(50px)` |
| `rotateX(angle)` | Поворот вокруг X | `rotateX(30deg)` |
| `rotateY(angle)` | Поворот вокруг Y | `rotateY(45deg)` |
| `rotateZ(angle)` | Поворот вокруг Z | `rotateZ(90deg)` |
| `perspective(n)` | Глубина перспективы | `perspective(1000px)` |

### 3.3. Примеры

**Поворот при наведении:**
```css
.icon {
  transition: transform 0.3s ease;
}

.icon:hover {
  transform: rotate(360deg);
}
```

**Увеличение карточки:**
```css
.card {
  transition: transform 0.3s ease;
}

.card:hover {
  transform: scale(1.05);
}
```

**Комбинированные трансформации:**
```css
.element {
  transform: translateX(50px) rotate(45deg) scale(1.2);
}
```

---

## 4. Комбинация `transition` и `transform`

### 4.1. Преимущества
- Высокая производительность (используется GPU)
- Плавность анимации
- Простота реализации

### 4.2. Типичные паттерны

**Кнопка с эффектом подъёма:**
```css
.button {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.button:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}
```

**Карточка с переворотом:**
```css
.card {
  transition: transform 0.6s ease;
  transform-style: preserve-3d;
}

.card.flipped {
  transform: rotateY(180deg);
}
```

**Появление элемента:**
```css
.element {
  opacity: 0;
  transform: translateY(20px);
  transition: 
    opacity 0.5s ease,
    transform 0.5s ease;
}

.element.visible {
  opacity: 1;
  transform: translateY(0);
}
```

---

## 5. Практические рекомендации

### 5.1. Производительность
**Анимируйте только:**
- `transform`
- `opacity`

**Избегайте анимации:**
- `width`, `height`
- `margin`, `padding`
- `top`, `left`

### 5.2. Доступность
- Учитывайте пользователей с предпочтением уменьшенной анимации:
```css
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
  }
}
```

### 5.3. Совместимость
- Используйте вендорные префиксы для старых браузеров:
```css
.element {
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  transform: rotate(45deg);
}
```

---

## 6. Практические задания

### Задание 1: Анимированная кнопка
Создайте кнопку, которая при наведении:
- Меняет цвет фона
- Увеличивается на 10%
- Поднимается на 2px

### Задание 2: Карусель изображений
Реализуйте горизонтальную прокрутку изображений с плавным переходом при клике на кнопки навигации.

### Задание 3: Модальное окно
Создайте модальное окно с анимацией появления (fade-in + slide-up).

---

## 7. Заключение

Свойства `transition` и `transform` являются фундаментальными инструментами CSS-анимации. Их правильное использование позволяет создавать производительные и визуально привлекательные интерфейсы без необходимости применения JavaScript или тяжёлых библиотек анимации.
```
