
# Занятие 3: Введение в программирование в Unity — скрипты, стрельба и мишени

## Цель занятия
Научиться создавать и подключать C# скрипты, сделать рабочую стрельбу и систему мишеней. К концу урока тир должен быть интерактивным.

### Шаг 1: Создание первой папки для скриптов
1. В окне **Project** зайдите в Assets.
2. Правой кнопкой мыши → **Create** → **Folder**. Назовите папку `Scripts`.

### Шаг 2: Создание скрипта для мишени (Target.cs)
1. В папке Scripts правой кнопкой → **Create** → **C# Script**. Назовите `Target`.
2. Откройте скрипт двойным кликом (откроется Visual Studio или другой редактор).

```csharp
using UnityEngine;

public class Target : MonoBehaviour
{
    public int points = 10;           // Сколько очков даёт мишень
    public ParticleSystem hitEffect;  // Эффект при попадании (можно оставить пустым)

    public void Hit()
    {
        // Создаём эффект попадания
        if (hitEffect != null)
            Instantiate(hitEffect, transform.position, Quaternion.identity);
        
        // Уничтожаем мишень через 0.3 секунды
        Destroy(gameObject, 0.3f);
        
        // Позже здесь будет добавление очков
        Debug.Log("Попадание! +" + points + " очков");
    }
}
```

3. Сохраните скрипт.

### Шаг 3: Создание скрипта оружия (SimpleGun.cs)
Создайте новый скрипт `SimpleGun.cs`:

```csharp
using UnityEngine;

public class SimpleGun : MonoBehaviour
{
    public float range = 100f;
    public AudioSource shotSound;     // Звук выстрела (добавьте позже)

    void Update()
    {
        // Стрельба по левой кнопке мыши или кнопке контроллера
        if (Input.GetButtonDown("Fire1") || Input.GetKeyDown(KeyCode.JoystickButton0))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        shotSound?.Play();
        
        Ray ray = new Ray(transform.position, transform.forward);
        if (Physics.Raycast(ray, out RaycastHit hit, range))
        {
            Target target = hit.transform.GetComponent<Target>();
            if (target != null)
            {
                target.Hit();
            }
        }
    }
}

```


### Шаг 4: Подключение скриптов к объектам
1. Все мишени выделите и добавьте компонент **Target** (Add Component → Target).
2. На объект Camera (или Player) добавьте компонент **SimpleGun**.
3. Создайте Particle System для эффекта попадания и назначьте его в поле `hitEffect`.

### Шаг 5: Создание ScoreManager (система очков)
Создайте скрипт `ScoreManager.cs` и подключите к Canvas (создайте UI позже).

### Шаг 6: Тестирование и отладка
1. Нажмите Play.
2. Проверьте стрельбу.
3. Сделайте Build и протестируйте в VR Box с контроллером.

**Задания для самостоятельной работы (много!):**
- Добавьте разное количество очков в зависимости от типа мишени.
- Сделайте мишени исчезать с анимацией (Scale down).
- Добавьте звук попадания.
- Сделайте ограниченное количество патронов.
- Создайте таймер раунда.

**Результат занятия:** Полностью рабочий интерактивный VR-Тир с стрельбой и очками.
