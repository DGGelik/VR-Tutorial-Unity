# Занятие 3: Первые скрипты — стрельба и мишени

## Создаём скрипты

### 1. Target.cs
```csharp
using UnityEngine;

public class Target : MonoBehaviour
{
    public int points = 10;
    
    public void Hit()
    {
        // Эффект попадания
        Destroy(gameObject, 0.5f);
        // TODO: добавить Particle System
    }
}
```

### 2. Gun.cs (простая стрельба)
```csharp
using UnityEngine;

public class Gun : MonoBehaviour
{
    public float range = 100f;
    
    void Update()
    {
        if (Input.GetButtonDown("Fire1")) // или Cardboard trigger
        {
            Shoot();
        }
    }
    
    void Shoot()
    {
        Ray ray = new Ray(transform.position, transform.forward);
        if (Physics.Raycast(ray, out RaycastHit hit, range))
        {
            Target target = hit.transform.GetComponent<Target>();
            if (target != null) target.Hit();
        }
    }
}
```

## Что делать
- Добавь скрипты на оружие и мишени.
- Протестируй в Play Mode.

**Домашнее задание:** Сделай чтобы мишени исчезали при попадании.
