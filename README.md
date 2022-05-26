# Контрольная работа. Часть 1.

## Задание 1. LRU cache.

<b>Теория</b>

Будем под кешированием понимать сохранение результатов вычислений в ответ на некоторые запросы. 
То есть, повторный результат запроса не всегда вычисляется заново, но иногда берется из таблицы, называемой кешем.
Сложно переоценить роль кеширования в современных системах. При этом часто возникает проблема, связанная с недостатком памяти. 
Действительно, что делать, если запросов много, а памяти хватает лишь для хранения ограниченного числа результатов? 
В этом случае, как правило, кеш строится следующим образом. Фиксируется размер кеша, пусть будет N, и 
сохраняются результаты только для N самых «популярных» запросов.

LRU (least recently used) - это алгоритм, при котором вытесняются значения, которые дольше всего не запрашивались. Соответственно, 
необходимо хранить время последнего запроса к значению (время можно сымитировать, например, порядком храния элементов). 
И, как только число закешированных значений превосходит N, необходимо вытеснить из кеша значение, которое дольше всего не запрашивалось.

<b>Задание</b>

Разработайте шаблонную структуру данных, которая удовлетворяет ограничениям LRU cache:
1. `LRUCache(int capacity)` - инициализирует вместимость LRU cache положительным числом.
2. `std::optional<V> get(K key)` - возвращает значение ключа, если он существует, иначе возвращает std::nullopt.
3. `void put(K key, V value)` - обновляет значение `value` для ключа `key`, если такой ключ существует. Иначе добавляет key-value пару в кеш. 
Если количество ключей превышает вместимость, удаляет ключ, который не использовался дольше всех.

<b>Пример</b>
```
LRUCache<int, int> lRUCache(2);
lRUCache.put(1, 1); // кеш равен {1=1}
lRUCache.put(2, 2); // кеш равен {1=1, 2=2}
lRUCache.get(1);    // возвращает 1
lRUCache.put(3, 3); // удаляется ключ 2, т.к. дольше всего не использовался, кеш равен {1=1, 3=3}
lRUCache.get(2);    // returns std::nullopt (ключ не был найден)
lRUCache.put(1, 4); // кеш равен {1=4, 3=3}
lRUCache.put(5, 5); // удаляется ключ 3, т.к. дольше всего не использовался, кеш равен {1=4, 5=5}
```

<b>Дополнительно</b>

Для реализации структуры вам может пригодиться std::map или какой-нибудь линейный контейнер (vector, ...), содержащий пары ключ-значение. 
