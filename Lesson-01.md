# Занятие 1: Введение в Unity + Первый прототип VR-Тира

## Цель
Запустить Unity, познакомиться с интерфейсом и сделать самый простой прототип тира.

## Пошаговая инструкция

1. **Установка**
   - Установи Unity Hub.
   - Добавь модуль Android Build Support.
   - Создай новый проект **3D (URP)** с названием `Unity-Tir-Course`.

2. **Интерфейс**
   - Изучите окна: Scene, Game, Hierarchy, Inspector, Project.

3. **Создание сцены**
   - Создай новую сцену `VR_Tir_Main`.
   - Удали Directional Light и Main Camera (мы добавим свои).

4. **Простая локация**
   - Создай Plane (пол).
   - Добавь Cube как мишень (масштаб 1x1x0.2, красный материал).
   - Добавь Skybox (Assets → Create → Material → Skybox).

5. **Камера для VR**
   - Добавь XR Rig (или Main Camera + Tracked Pose Driver для Cardboard).

6. **Первый Build**
   - File → Build Settings → Android → Switch Platform.
   - Player Settings → XR Plug-in Management → Cardboard.
   - Build And Run.

## Домашнее задание
Сделай build и протестируй в Cardboard. Пришли скриншот.

**Следующее занятие:** Создаём полноценную комнату тира.
