# LunarLander-v3_SANE

Этот проект демонстрирует применение алгоритма SANE (Symbiotic, Adaptive Neuro-Evolution) для обучения агента успешной посадке в среде Lunar Lander.

Алгоритм SANE (Symbiotic, Adaptive Neuro-Evolution) — это метод эволюции нейронных сетей, при котором:
* эволюционируются отдельные нейроны, а не вся сеть целиком;
* нейроны случайно комбинируются в полные сети;
* каждая комбинация оценивается в среде (в нашем случае — посадка лунохода);
* на основе оценок нейронов проводится естественный отбор.

## Структура кода

-   **Класс `Neuron`:** Представляет отдельный нейрон скрытого слоя с весами, смещением и метрикой фитнеса. Содержит методы для активации (`activate`) и мутации (`mutate`).
-   **Класс `Network`:** Собирает нейронную сеть из выбранных нейронов скрытого слоя и фиксированного выходного слоя. Содержит метод `forward` для прохождения прямого распространения и выбора действия на основе состояния среды.")
-   **Функция `initialize_population`:** Создает начальную популяцию нейронов с случайными параметрами.
-   **Функция `create_random_network`:** Случайно выбирает подмножество нейронов из популяции для создания экземпляра класса `Network`.
-   **Функция `evaluate_network`:** Оценивает производительность данной сети в среде Lunar Lander, запуская один или несколько эпизодов и возвращая суммарную награду и финальное состояние.
-   **Функция `evolve`:** Реализует один шаг эволюции. Она создает и оценивает несколько сетей, обновляет фитнес нейронов на основе их участия в этих сетях (с учетом специфического посадочного балла), отбирает лучших нейронов в пул размножения и создает новое поколение мутировавших нейронов.
-   **Основной цикл обучения:** Итерирует по заданному количеству поколений, вызывая функцию `evolve` для обновления популяции нейронов и отслеживая производительность лучшей сети в каждом поколении.
-   **Функции визуализации (`visualize_episode`, `visualize_neuron_activations`):** Позволяют просмотреть работу финальной обученной сети в среде и визуализировать активации нейронов скрытого слоя в течение эпизода.

## Установка

Для запуска проекта требуются Python и следующие библиотеки:

1. Установите `swig`:
```bash
!apt install swig -y -q
```

2. Установите `gymnasium` с поддержкой Box2D:
```bash
!pip install gymnasium[box2d] -q
```

## Результаты и визуализация

После завершения обучения вы сможете увидеть результаты в виде:

### График истории награды
График 'SANE обучение лунохода' показывает, как изменялась лучшая награда, достигнутая агентом в среде, на протяжении поколений обучения. Ожидается, что со временем лучшая награда будет увеличиваться, демонстрируя процесс обучения алгоритма.

### Визуализация эпизодов
Проект включает визуализацию эпизодов игры Lunar Lander:
*   **Эпизод до обучения:** Демонстрирует случайное поведение агента, управляемого сетью со случайными весами, до начала эволюции.
*   **Эпизод после обучения:** Показывает поведение агента, управляемого лучшей сетью, найденной в результате эволюции. Цель — увидеть успешную или улучшенную попытку посадки.
