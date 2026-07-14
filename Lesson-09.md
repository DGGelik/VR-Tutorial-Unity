
# Занятие 9: Интерактивные компоненты. Столкновения, касания и поведение объектов

## Цель занятия
Добавить физику, столкновения и более сложное поведение мишеней.

### Шаг 1: Добавление физики к мишеням
1. Выделите префаб мишени.
2. Добавьте компонент **Rigidbody** (Add Component → Physics → Rigidbody).
3. Поставьте:
   - Use Gravity = true
   - Is Kinematic = false
4. Добавьте **Box Collider** или **Mesh Collider** (для точности).

### Шаг 2: Улучшение скрипта попадания
Обновите `Target.cs`:

```csharp
public void Hit()
{
    Rigidbody rb = GetComponent<Rigidbody>();
    if (rb != null)
    {
        rb.AddForce(Vector3.up * 300f); // подбрасываем мишень
    }
    
    // остальной код...
}
```

### Шаг 3: Добавление Particle System для попадания
1. **GameObject** → **Effects** → **Particle System**.
2. Настройте:
   - Duration = 0.5
   - Start Size = 0.2
   - Emission Rate = 50
3. Сделайте его префабом и назначьте в `Target.cs`.

### Шаг 4: Создание разных типов мишеней
1. Создайте 3 префаба:
   - StaticTarget
   - MovingTarget (добавьте скрипт движения)
   - BonusTarget (больше очков)

### Шаг 5: Простое движение мишеней
Создайте скрипт `MovingTarget.cs`:

```csharp
using UnityEngine;

public class MovingTarget : MonoBehaviour
{
    public float speed = 2f;
    public Vector3 direction = Vector3.right;

    void Update()
    {
        transform.Translate(direction * speed * Time.deltaTime);
    }
}
```

### Шаг 6: Тестирование
Сделайте Build и проверьте в VR Box и AR, чтобы мишени падали, двигались и реагировали на попадания.

**Результат:** Динамичный и интересный тир с физикой и разными типами мишеней.
