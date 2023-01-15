## Проект по извлечению ключевых слов из текста, их семантическому анализу и тегированию корпуса текстов

**Цель:** разработка системы, выделяющей ключевые слова (n-граммы) в тексте публикации и оценивающей их семантическое сходство со словами в заголовках и тегах; На основании полученных данных система выделяет наиболее подходящие для каждого текста ключевые слова и визуализирует их как часть общего для корпуса облака тегов.

**Поддерживаемые языки:** русский.

**Перспективы использования** – выявление ошибочно использованных, повторяющихся и пересекающихся тегов, выявления тематического несоответствия заголовков и текстов публикаций. Визуализация нового облака тегов.

**Перспективы дальнейшей разработки** – Поиск дубликатов тегов именованных сущностей с помощью средств NER. Добавление средств для обработки текста на английском языке.

**Уточнение цели:** публикации в интернете часто сопровождаются тегами для упрощения поисковых задач. В качестве примеров предлагается рассмотреть сайт [SecurityLab.ru](https://www.securitylab.ru/), посвященный кибербезопасности и [ICT.Moscow](https://ict.moscow/), посвященный ИКТ в целом. Все материалы сайтов открыты для импользования.

В работе с публикациями выявляются такие ошибки, как употребление тегов, несоответствующих теме текста, а также наличие излишних и повторяющихся тегов. Примеры выявленных ошибок представлены в файле EXAMPLE.md. Проблема неправильных тегов может усугубляться при их автоматической расстановке без импользования комплексных средств NLP и затруднять поиск информации на сайте.

Предполагается разработать систему, которая выполнит следующие задачи:
- формирование текстового корпуса публикаций;
- выделение ключевых n-грамм в тексте средствами анализа (RAKE, TF-IDF, nBERT);
- фильтрация ключевых n-грамм с помощью грамматических паттернов Spacy;
- Сравнение семантического сходства ключевых n-грамм и содержимого соответствующих тегов и заголовков с помощью векторного представления слов (Rusvectores или Navec);
- визуализация облака ключевых слов корпуса.

На основании результатов работы системы предполагается выявить случаи неправильного использования тегов и оглавления, а также сформировать новое облако тегов для корпуса текстов, которое облегчит пользовательскую навигацию на интернет-сайте.

>Следует отметить, что интернет-ресурс [SecurityLab.ru](https://www.securitylab.ru/) в целом посвящен теме кибербезопасности, что ставит под сомнение перспективы использования метрики TF-IDF для выявления ключевых слов в его содержимом. В связи с этим предполагается использовать для решения этой задачи алгоритм RAKE. 

>Дополнительной задачей может стать сравнение эффективности библиотек RAKE-nltk, Gensim и keyBert, а также моделей Rusvectores и Navec в работе системы.

**Аналитика:** для решения поставленной задачи – выделения лишней информации в тексте используются программные модели на основе метрики RAKE, а также модели, создающие векторное представление текстов: Rusvectores или Navec.

**Лингвистический компонент:**
- корпус собирается из новостных материалов информационного сайта [SecurityLab.ru](https://www.securitylab.ru/), посвященного кибербезопасности;
- объем корпуса составляет 2000 текстов. Тексты загружаются с помощью парсера;
- препроцессинг: удаление пунктуации, лемматизация, токенизация и удаление стоп-слов.

**Входные данные:** файл CSV, содержащий таблицу с текстами, подлежащими анализу (колонки: заголовок, дата, теги, текст).

**Выходные данные:** файл CSV, содержащий таблицу с текстами (колонки: заголовок, дата, n-граммы, оригинальные теги, текст); Изображение в формате png, сожержащее визуализацию облака ключевых слов-тегов для корпуса.

**Тестирование:** все публикации [SecurityLab.ru](https://www.securitylab.ru/) сопровождаются тегами и заголовками. Таким образом, пользователь имеет возможность сравнить соответствие оригинальных тегов, заголовков и выделенных системой ключевых слов с помощью векторных моделей. Предполагается выделить для каждого текста пять ключевых n-грамм и исследовать их семантическое сходство с n-граммами в заголовках и тегах публикаций. 

**Использование технических навыков:** сбор собственного корпуса, препроцессинг текстов, создание списков лемм, выделение ключевых слов по метрике RAKE, проверка наличия выделенных ключевых слов в соответствующих им заголовках и тегов, оценка их семантического сходства.

**Порядок работы:**
- разработка парсера (загрузчика текстов) для сайта [SecurityLab.ru](https://www.securitylab.ru/) на основе библиотеки Beautifulsoup;
- создание текстового корпуса из новостных публикаций;
- разработка функции выделения ключевых слов из текстов с помощью библиотеки RAKE-nltk;
- разработка функции грамматической фильтрации средствами библиотеки Spacy;
- разработка функции фильтрации на основе семантического сходства с помощью модели Rusvectores или Navec;
- создание функции визуализации облака ключевых слов с помощью библиотеки mathplotter;
- создание общей функции выделения ключевых слов;
- 
-  *дополнительно: разработка функций выделения ключевых слов с помощью Gensim и KeyBERT;
 
### Ссылки 

**извлечение ключевых слов**

[Описание алгоритмов для выделения ключевых слов: Rake, YAKE!, TextRank](https://vc.ru/newtechaudit/449493-algoritmy-dlya-vydeleniya-klyuchevyh-slov-rake-yake-textrank)

[Пример сравнительного использования алгоритмов Rake и keyBERT, а также грамматическая фильтрация средствами Spacy](https://towardsdatascience.com/keyword-extraction-a-benchmark-of-7-algorithms-in-python-8a905326d93f)

**Векторное представление слов**

[Проект Natasha](https://github.com/natasha)

[Описание проекта Natasha](https://habr.com/ru/post/516098/)

[Дополнительное описание проекта Natasha](https://habr.com/ru/post/349864/)

[Rusvectores - библиотека вложений](https://rusvectores.org/ru/models/)

[Navec - коллекция предобученных вложений проекта Natasha](https://github.com/natasha/navec)

**Визуализация ключевых слов**

[Визуализация вложений Word2Vec в Word с помощью t-SNE](https://machinelearningmastery.ru/google-news-and-leo-tolstoy-visualizing-word2vec-word-embeddings-with-t-sne-11558d8bd4d/)

**извлечение именованных сущностей**

[Описание проекта NRLPK](https://habr.com/ru/post/468141/)
[проект NRLPK](https://github.com/avl33/nrlpk)

**Дополнительно**

[Word2Vec: как работать с векторными представлениями слов](https://neurohive.io/ru/osnovy-data-science/word2vec-vektornye-predstavlenija-slov-dlja-mashinnogo-obuchenija/)

[Обучаем Word2vec: практикум по созданию векторных моделей языка](https://sysblok.ru/knowhow/obuchaem-word2vec-praktikum-po-sozdaniju-vektornyh-modelej-jazyka/)

[библиотека проекта Natasha](https://natasha.github.io/corus/)

[открытый датасет Lenta.ru](https://github.com/yutkin/Lenta.Ru-News-Dataset)

[корпус Taiga](https://tatianashavrina.github.io/taiga_site/)

[датасет РИА Новости](https://github.com/RossiyaSegodnya/ria_news_dataset)
