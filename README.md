# CV Skills

Репозиторий содержит два связанных skill для подготовки к поиску работы и собеседованиям:

- [`career-grill`](skills/career-grill/README.md) — строит и помогает защитить карьерную легенду по одной роли;
- [`career-cv`](skills/career-cv/README.md) — превращает подтверждённый опыт из легенды в ATS-сильные CV-bullets по пользовательскому списку ключевых фраз.

Рекомендуемый порядок: сначала проработать роль через `career-grill`, затем передать `career-cv` список ключевых фраз и подготовить её секцию резюме.

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
    └── agents/
```
