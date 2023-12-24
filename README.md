# Solution-for-recommending-matches-between-customer-and-dealer-products

Проектное участие в кросс-функциональном хакатоне по разработке ML-продукта и интерфейса модели сопоставления товаров ООО “Просепт”

## Задача
Разработка ML-продукта, которое автоматизирует процесс сопоставления товаров заказчика с размещаемыми товарами дилеров.

## Что было сделано
Был выполнен предварительный анализ данных, включая выявление пропусков и дубликатов. Текст был очищен от стоп-слов, знаков пунктуации и цифр. Также были исправлены опечатки, проведена векторизация текста с использованием методов tf-idf и LaBSE. Были выделены дополнительные признаки, такие как объем товара и цена.

Предварительная обработка текста была структурирована в отдельные функции в Python-скрипте. Для измерения схожести текстов применялись алгоритмы cosine similarity и библиотека FAISS. 

В качестве метрики качества была выбрана accuracy@k, что позволяет оценить точность модели при предсказании верного ответа среди первых k рекомендаций. Метрика показывает отношение количества запросов с подходящей рекомендацией среди k рекомендаций ко всем запросам.

Для полученого алгоритма получили:

* accuracy@5 = 0.95
* accuracy@3 = 0.91
* accuracy@7 = 0.96

## Решение

Предоставлен скрипт на языке Python с функцией _get_recommendations_ в файле _model.py_. Эта функция принимает входные данные, включая индекс запроса из таблицы данных от дилеров (marketing_dealerprice), использует модуль preprocess для обработки названия, преобразует его в эмбеддинги с использованием модели 'sentence-transformers/LaBSE' и затем находит топ-k ближайших соседей из корпуса названий от Просепт. Результатом является список рекомендованных индексов для таблицы товаров от Просепт.
