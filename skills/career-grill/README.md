# Career Grill

`career-grill` последовательно строит защищаемую карьерную легенду для одной Node.js backend/fullstack-роли. Skill раскрывает проекты, архитектуру, личный scope, достижения и происхождение метрик, затем формирует атомарный `Паспорт для CV` с `Claim ID` и eligibility. Другие основные стеки пока не поддерживаются; интервью-вопросы и mock-интервью в процесс не входят.

Для Node.js-профиля skill также ведёт сквозную карту ключевых слов и микросервисных паттернов по всем компаниям. Паттерны попадают в легенду только как конкретные подтверждённые кейсы с механизмом и метрикой.

Встроенный рейтинг и список паттернов сохранены в [references/nodejs-international-keywords.md](references/nodejs-international-keywords.md).

## Установка

```bash
npx skills@latest add FOZERY/cv-skills \
  --skill career-grill \
  --copy \
  -y
```

## Запуск

```text
$career-grill
```

## Результат

- `CAREER_LEGEND.md` — единая карьерная легенда;
- `research/<company-slug>.md` — исследование активной компании;
- `research/market-and-location.md` — источники по международному маршруту;
- атомарный `Паспорт для CV` внутри каждой главы — единственный разрешённый источник claims для `career-cv`.
