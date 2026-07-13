# Занятие 5: Анимация и завершение VR-Тира

## Ключевые скрипты

### TargetSpawner.cs
```csharp
using UnityEngine;
using System.Collections;

public class TargetSpawner : MonoBehaviour
{
    public GameObject targetPrefab;
    public Transform[] spawnPoints;
    public float spawnInterval = 2f;
    
    void Start() => StartCoroutine(SpawnRoutine());
    
    IEnumerator SpawnRoutine()
    {
        while (true)
        {
            int index = Random.Range(0, spawnPoints.Length);
            Instantiate(targetPrefab, spawnPoints[index].position, Quaternion.identity);
            yield return new WaitForSeconds(spawnInterval);
        }
    }
}
```

## Что сделать на уроке
1. Добавь анимацию появления мишеней.
2. Реализуй систему очков.
3. Добавь звук выстрела и попадания.
4. Сделай финальный Build VR-Тира.

**Поздравляем!** У тебя готов полноценный **VR-Тир**.
