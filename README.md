# A first-level heading Легкие таймеры и интервалы для юнити

## A second-level heading Объявление класса
Для того чтобы это работало нужно:
1. Объявить переменную и зарегистрировать ваш таймер

```
  public class TestClass
  {
      private Timer _timer;
    
      private void Init()
      {
          _timer = Timer.Register(2f, () => Debug.Log("Timer is done"));
      }
  }
```
2. Во время регистрации вам откроется доступ к куче настроек, рассмотрим все по порядку:
```
public static Timer Register(float duration, Action onComplete, Action<float> onUpdate = null, Action<float> onTimeRemaining = null, bool isLooped = false, bool useRealTime = false, MonoBehaviour autoDestroyOwner = null)

duration - Время действия таймера
onComplete - коллбек выполнения
onUpdate - тик обновления таймера, возвращает float - сколько секунд прошло с запуска
onTimeRemaining - тик обновления таймера, возвращает float - сколько секунд таймера осталось
isLooped - будет ли зациклен ваш таймер(отправляет onComplete каждый цикл)
useRealTime - синхронизируется с реальным временем, игнорирует изменение Time.timescale
autoDestroyOwner - можно прикрепить к таймеру монобех, который он будет отслеживать, если монобех уничтожится, таймер остановиться
Почти все переменные можно переопределить после регистрации класса, этим тоже можно пользоваться

```

Пример простого использования таймера в 1 пункте, пример использования всех функций таймера ниже
```
    _testTimer = Source.Timer.Register(
        duration: 1f,
        onComplete: () =>
        { 
            Debug.Log(string.Format("Complete"));
        }       
        onUpdate: secondsElapsed =>
        {
            Debug.Log(string.Format("Timer run update callback: {0:F2} seconds", secondsElapsed));    
        },
        onTimeRemaining: timeRemaining =>
        {
            Debug.Log(string.Format("Timer run time remaining callback: {0:F2} seconds", timeRemaining));
        },
        isLooped: false,
        useRealTime: false);

duration и onComplete являются обязательными, остальные переменные можно менять по необходимости, просто объявив их как это сделано в примере выше
```

## A second-level heading Методы класса
### A third-level heading Функциональные методы 
Cancel - отмена таймера без вызова onComplete
Pause - остановка таймера
Resume - продолжение после остановки

Области применения +- те же, как и в UniRx, с остальным я думаю вы сможете разобраться сами

