
# Занятие 8: Основы разработки интерфейса AR/VR-приложения и игры

## Цель занятия
Научиться создавать удобный пользовательский интерфейс (очки, таймер, кнопки) для AR и VR тира.

### Шаг 1: Создание Canvas
1. В Hierarchy правой кнопкой → **UI** → **Canvas**.
2. В Inspector Canvas выберите **Render Mode**:
   - Для VR: **World Space**.
   - Для AR: **Screen Space - Overlay**.

### Шаг 2: Создание текста очков
1. На Canvas правой кнопкой → **UI** → **Text - TextMeshPro**.
2. Назовите объект `ScoreText`.
3. В Inspector:
   - Text = "Очки: 0"
   - Font Size = 48
   - Alignment = Center
   - Color = белый
4. Разместите текст в верхнем левом углу.

### Шаг 3: Создание таймера
1. Создайте ещё один TextMeshPro, назовите `TimerText`.
2. Разместите в верхнем центре.
3. Создайте скрипт `GameTimer.cs`:

```csharp
using UnityEngine;
using TMPro;
using UnityEngine.SceneManagement;

public class GameTimer : MonoBehaviour
{
    public float gameTime = 60f;
    public TextMeshProUGUI timerText;

    void Update()
    {
        gameTime -= Time.deltaTime;
        timerText.text = "Время: " + Mathf.Ceil(gameTime).ToString();

        if (gameTime <= 0)
        {
            // Можно добавить окончание игры
            Debug.Log("Время вышло!");
        }
    }
}
```

4. Добавьте скрипт на Canvas и перетащите `TimerText` в поле.

### Шаг 4: Создание кнопок
1. На Canvas → **UI** → **Button - TextMeshPro**.
2. Назовите `RestartButton`.
3. В Inspector кнопки найдите **On Click ()** → нажмите +.
4. Перетащите Canvas или пустой объект с менеджером и выберите функцию Restart.

### Шаг 5: Адаптация интерфейса под VR и AR
- Для VR: сделайте Canvas World Space и разместите перед игроком.
- Для AR: используйте Screen Space.

### Шаг 6: Сборка и тестирование
1. Сделайте Build.
2. Проверьте в VR Box и на AR-метке, чтобы интерфейс был виден и работал.

**Результат занятия:** У вас есть полноценный интерфейс с очками, таймером и кнопками.
