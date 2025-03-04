
#  Hot Dog Classifier зі Streamlit

## Огляд проєкту

Hot Dog Classifier - це веб-додаток, створений за допомогою Streamlit, який використовує модель машинного навчання для визначення, чи містить завантажене зображення хот-дог чи ні. Додаток демонструє функціональність моделі **julien-c/hotdog-not-hotdog**, розміщеної на платформі Hugging Face.

## Як це працює

Додаток дозволяє користувачу завантажити зображення через інтуїтивно зрозумілий інтерфейс. Після завантаження зображення, модель класифікації аналізує його та виводить результат з імовірностями для кожного класу ("хот-дог" або "не хот-дог").

## Технічні деталі

Веб-додаток побудований з використанням наступних технологій:

- **Streamlit** - фреймворк для створення інтерактивних веб-додатків на Python
- **Hugging Face Transformers** - бібліотека для роботи з моделями машинного навчання
- **Pillow (PIL)** - бібліотека для обробки зображень

## Структура проєкту

Проєкт складається з двох основних файлів:

1. **app.py** - основний файл додатку, що містить логіку та інтерфейс
2. **requirements.txt** - файл із залежностями, необхідними для роботи додатку

## Встановлення та запуск

Для запуску додатку локально потрібно:

1. Встановити залежності:
   ```
   pip install -r requirements.txt
   ```

2. Запустити Streamlit додаток:
   ```
   streamlit run app.py
   ```

## Код додатку

```python
import streamlit as st
from transformers import pipeline
from PIL import Image

pipeline = pipeline(task="image-classification", model="julien-c/hotdog-not-hotdog")

st.title("Hot Dog? Or Not?")

file_name = st.file_uploader("Upload a hot dog candidate image")

if file_name is not None:
    col1, col2 = st.columns(2)

    image = Image.open(file_name)
    col1.image(image, use_column_width=True)
    predictions = pipeline(image)

    col2.header("Probabilities")
    for p in predictions:
        col2.subheader(f"{ p['label'] }: { round(p['score'] * 100, 1)}%")
```

## Опис функціональності

1. Імпортуються необхідні бібліотеки: Streamlit для створення інтерфейсу, Transformers для роботи з моделлю машинного навчання, і PIL для обробки зображень.
2. Створюється об'єкт pipeline для задачі класифікації зображень з використанням моделі "julien-c/hotdog-not-hotdog".
3. Встановлюється заголовок додатку "Hot Dog? Or Not?".
4. Створюється віджет для завантаження файлу зображення.
5. Після завантаження зображення:
   - Сторінка розділяється на дві колонки
   - У першій колонці відображається завантажене зображення
   - Модель аналізує зображення та видає прогнози
   - У другій колонці відображаються результати класифікації з імовірностями

## Розгортання

Додаток можна розгорнути на платформі Hugging Face Spaces, яка забезпечує хостинг для Streamlit додатків. Готова версія цього додатку доступна за посиланням **NimaBoscarino/hotdog-streamlit**.

## Вимоги до системи

- Python 3.6 або вище
- Підключення до Інтернету (для завантаження моделі)
- Достатньо пам'яті для завантаження моделі машинного навчання

## Додаткові ресурси

- [Документація Streamlit](https://docs.streamlit.io/)
- [Transformers від Hugging Face](https://huggingface.co/docs/transformers/index)
- [Документація Hugging Face Spaces](https://huggingface.co/docs/hub/spaces-overview)
