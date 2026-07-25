# Fable 5's Code Review Rules

> 29 of 34 rules supplement Opus 5's default review; the remaining 5 it applies anyway.
>
> By Opus 5's own estimate — a judgement from reading the ruleset, not a measurement.
> По собственной оценке Opus 5 — суждение по прочтении набора, а не замер.

A compact ruleset that makes an LLM code review falsifiable instead of agreeable.
Компактный набор правил, который делает LLM-ревью проверяемым, а не покладистым.

---

<details>
<summary><b>EN — English</b></summary>

## How to use

Copy the rules text into your project's `CLAUDE.md`, or paste it into the prompt before asking for a review. You can use individual rules on their own, or the whole text. I did not strip out the rules Opus already applies: this is a complete survey of how the Fable model does review, and removing anything would misrepresent it. The survey was taken before the Opus 5 release. It was right after that release that people started complaining about a drop in Fable's "intelligence" and "review relevance". Thank you.

- `code-review-rules.en.md` — English
- `code-review-rules.ru.md` — Russian

In `CLAUDE.md` or in the prompt, the rules load at the start of the session and fire on any phrasing ("review this", "does this look OK?").

Not an official Anthropic material — these are model answers collected in a chat session.

## Why not to add more rules

Almost everything you will want to add after the fact is a disclosure rule. "State your confidence", "List the gaps", "Describe your coverage", "Name your assumptions". They look responsible, they are pleasant to write, and they are almost always true. The strength of this file lies in the opposite move:

> When you hit uncertainty — go and resolve it, don't describe it.

Disclosure and description rules are cheap to satisfy and indistinguishable in appearance from rigor. So they don't merely dilute — they shift the document's center of gravity from doing the work to narrating the work. Add enough of them and you get a review that reports flawlessly on everything it did not check.

</details>

---

<details>
<summary><b>RU — Русский</b></summary>

## Как использовать

Скопируйте текст правил в файл `CLAUDE.md` вашего проекта или вставьте в промпт перед запросом на ревью. Вы можете использовать отдельно какие-то правила или целиком весь текст. Я не стал убирать то, что и так есть в Opus, так как это полный опрос Fable модели о том, как он делает ревью, и было бы неправильно что-то убирать. Опрос модели Fable был до релиза Opus 5. Как раз после релиза Opus 5 люди начали ругаться на снижение «интеллекта» и «релевантности ревью» у Fable модели. Спасибо.

- `code-review-rules.ru.md` — русский
- `code-review-rules.en.md` — английский

В `CLAUDE.md` или промпте правила грузятся в начале сессии и срабатывают на любую формулировку («сделай ревью», «глянь, норм?»).

Не является официальным материалом Anthropic — это ответы модели, полученные в диалоге.

## Почему не стоит дописывать правила

Практически всё, что хочется добавить постфактум, — правила раскрытия. «Обозначь уверенность», «Перечисли пробелы», «Опиши покрытие», «Назови допущения». Они выглядят ответственно, их приятно писать, и они почти всегда истинны. Сила этого файла ровно в обратном ходе:

> При столкновении с неопределённостью — иди и разреши её, а не описывай.

Правила раскрытия/описывания дёшевы в исполнении и неотличимы по виду от строгости. Поэтому они не просто разбавляют — они смещают центр тяжести документа с работы на повествование о работе. Дописав их достаточно, ты получишь ревью, которое безупречно отчитывается о том, чего не проверило.

</details>
