# CV Skills

Репозиторий содержит два связанных skill для подготовки Node.js backend/fullstack-профиля:

- [`career-grill`](skills/career-grill/README.md) — приоритетно собирает защищаемый опыт и атомарный паспорт claims;
- [`career-cv`](skills/career-cv/README.md) — превращает разрешённые claims в короткие сильные CV-bullets по Node.js-профилю и вакансии.

Порядок обязателен: сначала `career-grill` раскрывает защищаемый опыт, затем `career-cv` использует только claims с `CV eligibility: allowed`. Интервью-вопросы, готовые ответы и mock-интервью этими skills не составляются.

## Установка с выбором skills

Команда обнаружит оба skill и предложит выбрать нужные skills и целевых агентов. Режим `--copy` устанавливает независимую копию skill.

```bash
npx skills@latest add FOZERY/cv-skills --copy
```

## Установка всех skills

```bash
npx skills@latest add FOZERY/cv-skills \
  --all \
  --copy \
  -y
```

Команды установки одного skill находятся в его README:

- [установка `career-grill`](skills/career-grill/README.md#установка);
- [установка `career-cv`](skills/career-cv/README.md#установка).

## Структура

```text
skills/
├── career-grill/
│   ├── README.md
│   ├── SKILL.md
│   └── references/
└── career-cv/
    ├── README.md
    ├── SKILL.md
    ├── agents/
    └── references/
```
