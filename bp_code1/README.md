## Чиним заказы — часть 1. Исправьте строку во фрагменте кода
Вы уже нашли место, где скрипт падает: проблема в строке, которая слишком жёстко пытается взять `order_id` из заказа.
Ниже показан короткий фрагмент того же скрипта с этой строкой. Исправьте её так, чтобы код больше не падал, если у заказа нет `order_id`. На этом шаге достаточно сделать получение значения безопаснее через `get()`

### Начальный код задания
```python
order = {"item": "Клавиатура"}

order_id = order["order_id"]  # исправьте эту строку
print(f"Заказ {order_id} отправлен в обработку")
```

### Эталонное решение эксперта
```python
order = {"item": "Клавиатура"}

order_id = order.get("order_id")
print(f"Заказ {order_id} отправлен в обработку")
```
### Ожидаемый ответ
```python
[
     "Заказ None отправлен в обработку"
]
```

### Подсказка:
Сейчас нужно поправить только одну строку. Не меняйте `print:` замените жёсткое получение `order_id` на более безопасное через `get()`.

### Тест:

```
import subprocess
from pathlib import Path

code = Path("main.py").read_text(encoding="utf-8")

assert 'order.get("order_id")' in code or "order.get('order_id')" in code, \
    "Используйте get(), чтобы программа не падала, если в заказе нет order_id."

result = subprocess.run(
    ["python", "main.py"],
    capture_output=True,
    text=True,
    encoding="utf-8"
)

assert result.returncode == 0, "После исправления программа должна выполняться без ошибки."

output = result.stdout.strip().splitlines()

expected = [
    "Заказ None отправлен в обработку"
]

assert output == expected, "Проверьте, что строка исправлена через get()."
```

