![hat of ReadME](https://github.com/haxbxbdbhshs/ReadMe-On-Ru-Lang-For-Palatine-Node/blob/main/hat.png)

# n8n-nodes-palatine-speech

---

> Разработано для бесшовной интеграции **Palatine Speech** в воркфлоу n8n.


Это community-нода n8n, которая интегрирует [Palatine Speech](https://speech.palatine.ru/) в ваш воркфлоу n8n, предоставляя возможность обрабатывать аудио файлы: проводить транскрибацию, диаризацию, анализ тональности и суммаризацию напрямую в воркфлоу n8n — без необходимости вручную настраивать HTTP-запросы.

## Навигация

---
[Поддерживаемые задачи (Tasks)](#поддерживаемые-задачи-tasks)\
[Установка](#установка)\
[Учётные данные (Credentials)](#учётные-данные-credentials)\
[Пример воркфлоу](#пример-воркфлоу)\
[Варианты использования](#варианты-использования) \
[Совместимость](#совместимость)\
[Полезные ресурсы](#полезные-ресурсы)\
[Ключевые слова](#ключевые-слова)


##  Поддерживаемые задачи (Tasks)

---
Подробнее о каждой задаче можно узнать из документации [Palatine Speech](https://docs.speech.palatine.ru/documentation/quick_start/transcription)
* [Полный список поддерживаемых файлов доступе по ссылке](https://docs.speech.palatine.ru/documentation/technical_information/supported_files)
* [Полный список поддерживаемых языков доступе по ссылке](https://docs.speech.palatine.ru/documentation/technical_information/supported_languages)

###  [Transcribe — транскрибация речи](https://docs.speech.palatine.ru/documentation/quick_start/transcription)

Транскрибация автоматически извлекает текст из записи и помогает оцифровать разговоры, лекции и звонки. Сервис рассчитан на работу с разными языками и определяет язык речи в аудио.


###  [Diarize — диаризация речи](https://docs.speech.palatine.ru/api-reference/diarization/diarization-polling-api/diarize)

Диаризация разделяет аудио на части по спикерам и показывает, кто из участников говорил в каждом фрагменте. На выходе получается разметка разговора, которую удобно использовать для протоколов и аналитики коммуникаций.

###  [Sentiment Analysis — анализ тональности](https://docs.speech.palatine.ru/documentation/quick_start/sentiment_analyze#sozdanie-zadachi)

Определяет эмоциональную окраску речи в аудио/видео (и умеет анализировать текст): возвращает отсортированный список классов с вероятностями, где первый элемент — самая вероятная тональность. Классы: `Very Negative`, `Negative`, `Neutral`, `Positive`, `Very Positive`

###  [Summarize — пересказ аудио](https://docs.speech.palatine.ru/documentation/quick_start/summarization)

Нода генерирует конспект/саммари по аудио (в т.ч. готовый сценарий `meeting_summary` со структурированным результатом), а также поддерживает функцию `user_prompt` — вы можете передать кастомный prompt к LLM, чтобы получить ответ в нужном стиле и формате (тезисы, решения/задачи, риски, Q&A и т.д.).


## Установка

---
1. В вашем экземпляре n8n перейдите в **Settings → Community Nodes → Install new**
2. Введите: `n8n-nodes-palatine-speech`
3. Нажмите **Install**
> ⚠️ Убедитесь, что переменная окружения `N8N_COMMUNITY_NODES_ENABLED=true` установлена.



## Учётные данные (Credentials)

---
1. Перейдите в **Credentials → + Create**
2. Найдите **Palatine Speech API**
3. Заполните поля:
  * **API Key** — доступен в личном кабинета Palatine Speech
  * **Base URL** — по умолчанию `https://api.palatine.ru` 
>  API-ключ находится в https://speech.palatine.ru/dashboard.


## Пример воркфлоу

---
1. `Webhook` → Получение аудиофайла
2. `Config` → Конфигурация параметров
3. `Palatine Speech` → Транскрибация файла
4. `Create record` → Создание записи в таблице
5. `Telegram` → Отправка результата в чат

![workflow example](https://github.com/haxbxbdbhshs/ReadMe-On-Ru-Lang-For-Palatine-Node/blob/main/WorkflowExample.png)

## Варианты использования

---
* **Итоги по встречам** \
Для записей встреч и интервью рекомендуется использовать `Summarize` (`meeting_summary`): формируется краткое резюме, перечень решений и задач; результат при необходимости направляется в командный чат.\
Для нестандартных запросов в `Summarize` укажите `Prompt` и задайте требуемую инструкцию, например: «Дополнительно структурируй договорённости по срокам и ответственным».
* **Конспекты лекций/вебинаров** \
Запись занятия → `Transcribe` → формирование дословной расшифровки. \
Полученный текст сохраняется в материалы занятия.
* **Авто-субтитры для видео**
Извлечение аудиодорожки → `Transcribe` + `Diarize` → подготовка субтитров и прикрепление к видео. \
`Transcribe` обеспечивает текстовую расшифровку, а `Diarize` добавляет разметку по спикерам.
* **Помощник тех поддержки** \
Обработка голосовых сообщений через `Sentiment Analysis` позволяет определить эмоциональную окраску обращения. \
На основе результата автоматически создаются тикеты в CRM и назначается приоритет обработки.
## Совместимость

---
Эта нода была протестирована на версиях n8n ≥ 1.39.1

## Полезные ресурсы

---
* [Документация Palatine Speech](https://docs.speech.palatine.ru/documentation/quick_start/transcription)
* [Руководство по Community Nodes в n8n](https://docs.n8n.io/integrations/community-nodes/)
* [Официальный GitHub n8n](https://github.com/n8n-io/n8n)

## Ключевые слова

---
`n8n-community-node-package`, `n8n`, `palatine`, `speech-to-text`, `transcribe`, `transcription`, `stt`, `audio`, `ai`, `automation`, `voice-to-text`, `speech-recognition`, `audio-transcription`, `audio2text`, `audio-processing`, `diarization`, `speaker-diarization`, `speaker-segmentation`, `summarization`, `audio-summarization`, `sentiment-analysis`, `emotion-detection`, `tone-analysis`

