# Fable 5's Code Review Rules

> 29 of 34 rules supplement Opus 5's default review; the remaining 5 it applies anyway.

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

</details>

---

<details>
<summary><b>RU — Русский</b></summary>

## Как использовать

Скопируйте текст правил в файл `CLAUDE.md` вашего проекта или вставьте в промпт перед запросом на ревью. Вы можете использовать отдельно какие-то правила или целиком весь текст. Я не стал убирать то, что и так есть в Opus, так как это полный опрос Fable модели о том, как он делает ревью, и было бы неправильно что-то убирать. Опрос модели Fable был до релиза Opus 5. Как раз после релиза Opus 5 люди начали ругаться на снижение «интеллекта» и «релевантности ревью» у Fable модели. Спасибо.

- `code-review-rules.ru.md` — русский
- `code-review-rules.en.md` — английский

В `CLAUDE.md` или промпте правила грузятся в начале сессии и срабатывают на любую формулировку («сделай ревью», «глянь, норм?»).

</details>
