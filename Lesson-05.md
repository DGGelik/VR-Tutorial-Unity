
# Занятие 5: Основы анимации в Unity. Скриптинг и интерактивность в мобильном VR

## Цель занятия
Научиться создавать анимацию, спавнер мишеней и завершить полноценный VR-Тир. К концу урока у вас должна быть игра с появляющимися мишенями, очками и звуками.

### Шаг 1: Создание системы очков (ScoreManager)
1. В папке Scripts создайте новый скрипт `ScoreManager.cs`.
2. Откройте его и вставьте следующий код:

```csharp
using UnityEngine;
using TMPro; // Для красивого текста

public class ScoreManager : MonoBehaviour
{
    public static int score = 0;           // Общий счёт
    public TextMeshProUGUI scoreText;      // Текст на экране

    public void AddPoints(int points)
    {
        score += points;
        if (scoreText != null)
            scoreText.text = "Очки: " + score.ToString();
    }
}
```

3. Создайте Canvas: **GameObject** → **UI** → **Canvas**.
4. На Canvas создайте Text — TextMeshPro (правой кнопкой на Canvas → UI → Text - TextMeshPro).
5. Перетащите этот текст в поле `scoreText` компонента ScoreManager.

### Шаг 2: Улучшение скрипта Target
Откройте `Target.cs` и обновите его:

```csharp
using UnityEngine;

public class Target : MonoBehaviour
{
    public int points = 10;
    public ParticleSystem hitEffect;

    public void Hit()
    {
        if (hitEffect != null)
            Instantiate(hitEffect, transform.position, Quaternion.identity);

        ScoreManager scoreManager = FindObjectOfType<ScoreManager>();
        if (scoreManager != null)
            scoreManager.AddPoints(points);

        Destroy(gameObject, 0.3f);
    }
}
```

### Шаг 3: Создание спавнера мишеней (TargetSpawner.cs)
Создайте новый скрипт `TargetSpawner.cs`:

```csharp
using UnityEngine;
using System.Collections;

public class TargetSpawner : MonoBehaviour
{
    public GameObject[] targetPrefabs;     // Разные мишени
    public Transform[] spawnPoints;        // Точки появления
    public float spawnInterval = 1.8f;     // Как часто появляются
    public float gameTime = 60f;           // Длительность раунда

    private float endTime;

    void Start()
    {
        endTime = Time.time + gameTime;
        StartCoroutine(SpawnRoutine());
    }

    IEnumerator SpawnRoutine()
    {
        while (Time.time < endTime)
        {
            int randomPrefab = Random.Range(0, targetPrefabs.Length);
            int randomPoint = Random.Range(0, spawnPoints.Length);

            Instantiate(targetPrefabs[randomPrefab], 
                        spawnPoints[randomPoint].position, 
                        Quaternion.identity);

            yield return new WaitForSeconds(spawnInterval);
        }
    }
}
```

### Шаг 4: Настройка спавнера
1. Создайте пустой объект `TargetSpawner`.
2. Добавьте на него компонент `TargetSpawner`.
3. Создайте 4–6 пустых объектов как точки спавна и перетащите их в массив `spawnPoints`.
4. Перетащите префабы мишеней в массив `targetPrefabs`.

### Шаг 5: Добавление звука
1. На объект Gun добавьте компонент **Audio Source**.
2. Перетащите звуковой файл выстрела в поле `shotSound`.
3. То же самое сделайте для попадания.

### Шаг 6: Финальная сборка и тестирование
1. Настройте все компоненты.
2. Сделайте Build And Run.
3. Протестируйте в VR Box: мишени должны появляться, вы должны попадать, очки должны расти.

**Что должно работать к концу урока:**
- Мишени появляются автоматически.
- При попадании начисляются очки.
- Есть звук выстрела.
- Игра длится 60 секунд.

Это завершение базового **VR-Тира**.
