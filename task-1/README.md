# Задача 1

Коллега отправил вам файл, но вы нигде не можете найти константу VECTOR_NAME. Нужно восстановить ее, опираясь на этот блок кода.

```
const getVector = ({x, y}) => {
    if (x > y) {
        if (Math.abs(x / y) < THRESHOLD) return;
        return x > 0 ? 3 : 1;
    } else {
        if (Math.abs(y / x) < THRESHOLD) return;
        return y > 0 ? 2 : 0;
    }
};

let v = getVector({x: _x, y: _y});
if (v && VECTOR_NAME.indexOf(v) !== -1) {
    ev.emit('event.' + VECTOR_NAME[v]);
}

ev.on('event.up', () => {
    console.log('Восхитительно, что-то движется вверх!');
});
```

Ответ:

Поскольку в emit передается `'event.' + VECTOR_NAME[v]`, то `VECTOR_NAME[v]` - часть имени события. Мы видим, что ev.on обрабатывает событие `ev.up`, значит `VECTOR_NAME` собержит имена направлений (up,left,right,top).

Поскольку getVector возвращает числа от 0 до 3, то VECTOR_NAME - массив, а не объект. В этом же можно убедиться по использованию метода 

Остается разорбраться в каком порядке имена направлений находятся в массиве VECTOR_NAME.

x>y - вправо либо вниз
x>y && x>0 - вправо (индекс - 3)
x>y && x<=0 - вниз (инлдекс - 1)

else(x<=y) - влево или вверх
y>0 - вверх (индекс - 2)
иначе - влево (индекс - 0)

Также `VECTOR_NAME.indexOf(v)` - неверная кончтрукиця, так как v уже индекс. Надо написать `VECTOR_NAME[v]`

ИТОГО `VECTOR_NAME=['left','down','up','right']`
