---
tags:
  - GIT
---

1) **Изменен** 
   (Изменяете файлы вашей рабочей копии.)
   Получают те файлы которые были изменены но не были зафиксированы
   
2) **Индексирован**
   (Выборочно добавляете в индекс только те изменения, которые должны попасть в следующий коммит, добавляя тем самым снимки только этих изменений в индекс.)
   Состояние "Индексирован" получают те файлы которые которые готовы получить commit (добавлена текущяя версия файла в снимок)
   
3) **Зафиксирован**
   (Когда вы делаете коммит, используются файлы из индекса как есть, и этот снимок сохраняется в ваш каталог Git.)
   Файлы которые были измены и зафиксированы