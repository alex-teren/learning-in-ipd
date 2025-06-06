# Комплексний порівняльний аналіз: Підходи до навчання стратегій ІДВ

## Вступ

Ітеративна Дилема В'язня (ІДВ) є класичною моделлю для дослідження стратегічної взаємодії у багатоагентних системах. Вивчення результативних стратегій у цьому середовищі має важливе значення для розвитку теорії ігор, машинного навчання та штучного інтелекту. У цьому дослідженні проведено порівняльний аналіз трьох підходів до навчання стратегій для ІДВ: навчання з підкріпленням (PPO), еволюційної страттегії (CMA-ES) та трансформерної архітектури (Decision Transformer). Кожен з підходів реалізує різні принципи навчання та має власні переваги й обмеження.

## Резюме

Проведено експериментальне дослідження з уніфікованими параметрами та єдиним протоколом оцінювання для всіх підходів. За результатами оцінювання середньої результативності проти 7 класичних стратегій опонентів, найвищий показник продемонстрував підхід PPO (258.78 балів), далі йде еволюційний підхід (233.66 балів) та трансформер (217.03 балів). Кожен підхід характеризується відмінними показниками співпраці, адаптивності та інтерпретованості.

## Налаштування експерименту

**Апаратна платформа:**
- Процесор: Apple M1 Max
- Оперативна пам'ять: 32GB RAM

**Уніфіковані параметри:**
- Довжина гри: 100 раундів на гру
- Набір опонентів: TitForTat, AlwaysCooperate, AlwaysDefect, Random(p=0.5), Pavlov, Grudger, GTFT(p=0.1) (загалом 7 стратегій)
- Оцінювання: 20 матчів на опонента для Evolution/Transformer, 20 епізодів для PPO
- Випадкове зерно: 42 (однакове для всіх підходів)
- Матриця виплат: Стандартна ІДВ (3,1,5,0)

## Тривалість навчання

| Підхід | Час навчання |
|--------|--------------|
| PPO | 354.6 секунд (5.9 хв) |
| Еволюційний підхід | 300.6 секунд (5.0 хв) |
| Трансформер | 1115.51 секунд (18.6 хв) |

## Аналіз стратегічної результативності

Результати експерименту показують, що різні підходи до навчання формують відмінні стилі стратегічної поведінки. Кожен алгоритм демонструє власний баланс між результативністю, співпрацею та адаптивністю.

### Загальні метрики результативності

| Підхід | Середній бал | Діапазон балів | Середня співпраця | Варіативність співпраці |
|--------|--------------|----------------|-------------------|-------------------------|
| PPO | 258.78 | 99.0 - 496.0 | 33.5% | Висока (σ=0.323) |
| Еволюційний підхід | 233.66 | 99.62 - 400.0 | 40.1% | Висока (σ=0.275) |
| Трансформер | 217.03 | 29.44 - 421.52 | 63.0% | Помірна (σ=0.191) |

### Результативність проти конкретних опонентів

| Опонент | Бал PPO | Бал Еволюційного підходу | Бал Трансформера | Провідний підхід |
|---------|---------|---------------------------|------------------|-------------------|
| TitForTat | 250.0 | 263.08 | 262.44 | Еволюційний підхід |
| AlwaysCooperate | 496.0 | 400.0 | 421.52 | PPO |
| AlwaysDefect | 99.0 | 99.62 | 68.5 | Еволюційний підхід |
| Random | 249.11 | 234.93 | 194.58 | PPO |
| Pavlov | 250.0 | 263.04 | 265.38 | Трансформер |
| Grudger | 152.0 | 101.67 | 29.44 | PPO |
| GTFT | 315.36 | 273.31 | 277.32 | PPO |

## Детальний аналіз підходів

### PPO (Навчання з підкріпленням)

Підхід PPO забезпечує найвищу середню результативність серед розглянутих алгоритмів. Основною перевагою є здатність адаптуватися до різних типів опонентів, що дозволяє результативно використовувати слабкі сторони кооперативних стратегій (наприклад, AlwaysCooperate) та демонструвати конкурентоспроможність проти оборонних стратегій (Grudger, GTFT). Водночас, рівень співпраці залишається відносно низьким, що свідчить про схильність до експлуатації опонентів у відповідних сценаріях. Час навчання є помірним.

### Еволюційний підхід (CMA-ES)

Еволюційний підхід формує стратегію типу Memory-One, яка характеризується балансом між співпрацею та захистом. Алгоритм демонструє високу результативність проти взаємовідповідних стратегій (TitForTat, Pavlov) та забезпечує найкращі оборонні показники проти AlwaysDefect. Перевагою є прозорість та інтерпретованість параметрів стратегії. Час навчання є найменшим серед усіх підходів, що робить цей метод привабливим для задач з обмеженими ресурсами.

### Трансформер (Decision Transformer)

Трансформерна архітектура демонструє найвищий рівень співпраці та найменшу варіативність поведінки. Алгоритм досягає стабільних результатів у кооперативних сценаріях, але поступається конкурентним підходам у протистоянні агресивним опонентам (AlwaysDefect, Grudger). Основною перевагою є здатність підтримувати послідовну кооперативну поведінку, проте час навчання є найбільшим серед усіх підходів.

## Порівняння стратегічної адаптації

### Можливості розпізнавання опонентів

- PPO: Висока адаптивність, результативне використання слабких опонентів, конкурентоспроможність проти складних стратегій.
- Еволюційний підхід: Послідовна стратегічна поведінка, хороша взаємовідповідність, найкращі оборонні показники.
- Трансформер: Високий рівень співпраці, стабільність, обмежена результативність проти агресивних стратегій.

### Теоретико-ігрові характеристики

| Аспект | PPO | Еволюційний підхід | Трансформер |
|---------------------|-----|--------------------|-------------|
| Взаємовідповідність | Добре | Дуже добре | Добре |
| Використання опонентів | Дуже добре | Добре | Помірно |
| Оборона | Добре | Дуже добре | Слабко |
| Адаптивність | Дуже добре | Добре | Обмежено |
| Послідовність | Помірно | Добре | Дуже добре |

## Обчислювальні вимоги

| Метрика | PPO | Еволюційний підхід | Трансформер |
|---------|-----|-------------------|-------------|
| Час навчання | 354.6с (5.9 хв) | 300.6с (5.0 хв) | 1115.5с (18.6 хв) |
| Використання пам'яті | Помірне | Низьке | Високе |
| Обчислювальна складність | Помірна | Низька | Дуже висока |
| Масштабованість | Гарна | Дуже добра | Обмежена |

## Інтерпретованість

- Еволюційний підхід: Висока інтерпретованість завдяки явним параметрам стратегії Memory-One.
- PPO: Обмежена інтерпретованість через використання нейронної мережі.
- Трансформер: Найменша інтерпретованість через складність архітектури.

## Практичні рекомендації

- PPO доцільно використовувати у конкурентних середовищах, де важлива максимізація результативності.
- Еволюційний підхід є результативним для задач, що вимагають прозорості, швидкого навчання та балансу між співпрацею і захистом.
- Трансформер рекомендовано застосовувати у кооперативних або освітніх сценаріях, де цінується стабільна співпраця.

## Висновки

Проведене дослідження показало, що жоден з підходів не є універсально найкращим для всіх сценаріїв. Вибір методу має ґрунтуватися на вимогах до результативності, інтерпретованості, швидкості навчання та характеру середовища. Розроблена уніфікована методологія оцінювання дозволяє об'єктивно порівнювати різні підходи та формувати рекомендації для практичного застосування. Подальші дослідження можуть бути спрямовані на розробку гібридних систем, що поєднують переваги розглянутих методів. 