# Исследование надёжности заёмщиков
Входные данные  — статистика о платёжеспособности клиентов. Нужно разобраться, как некоторые факторы, например семейное положение и количество детей клиента влияет на погашения кредита в срок.
 
Результаты исследования будут учтены при построении модели **кредитного скоринга** — специальной системы, которая оценивает способность потенциального заёмщика вернуть кредит банку.
 
В ходе первичного знакомства с данными, предоставленными заказчиком, статистики о платёжеспособности клиентов, стало видно, что в некоторых столбцах требуется обработать пропуски, заменить значения на целочисленные, преобразовать отрицательные значения в положительные, обработать дубликаты и изменить типы данных.
 
Пропущенные значения  в total_income и days_employed могут говорить о том, что клиент официально или вовсе не трудоустроен.
Заполнение обоих столбцов взаимосвязано. В случае, если клиент официально или вовсе не трудоустроен значение в графе ежемесячный доход не заполняется. Но с другой стороны это может быть техническая ошибка. По инициативе заказчика, было принято решение заменить пропуски в в total_income медианным значением по столбцу, потому что пропуски в количественных переменных заполняют характерными значениями. Это значения, характеризующие состояние выборки, — набора данных, выбранных для проведения исследования. Чтобы примерно оценить типичные значения выборки, годятся среднее арифметическое или медиана.
 
Касаемо признака стажа (days_employed). При подсчете среднего стажа по типам занятости, видно, что имеются аномалии положительного и отрицательного стажа. Что примечательно, положительный стаж только у некоторых типов занятости + он же выглядит слишком большим. Поэтому большой стаж поделила на 24, потом на 365, так как похоже на то, что он попросту измерялся в часах. Для адекватных типов занятости мы просто делим на 365. Таким образом, создается новый признак стажа в годах. Затем избавились от отрицательных значений, и заполнили пропуски медианными значениями.
 
В столбцах возраст и пол найдены нелогичные данные, например, 0 лет или пол XBA. Строки, в которых возраст 0, были заменены на медианные значения, в зависимости от семейного положения.
 
Были выявлены дубликаты в данных, после проработки методом str.lower() кол-во дублей увеличилось. Возможно возникли по причине ручного ввода поля образование, при заполнении использовался разный регистр букв.
 
В связи с тем, что поле цель кредита заполнялось произвольным текстом из всей массы целей с помощью лемматизации удалось выделить четыре основные, для это пришлось импортировать библиотеку для получения леммы на русском языке. Это помогло понять, что наиболее популярная цель кредита связана с недвижимостью, это может быть: улучшение жилищных условий, покупка дополнительного жилья с целью ведения коммерческой деятельности. В связи с тем, что поле цель кредита заполнялось произвольным текстом из всей массы целей с помощью лемматизации удалось выделить четыре основных, для это пришлось импортировать библиотеку для получения леммы на русском языке. Это помогло понять, что наиболее популярная цель кредита связана с недвижимостью, это может быть: улучшение жилищных условий, покупка дополнительного жилья с целью ведения коммерческой деятельности.
## Вывод
Люди, которые состоят в официальном браке, и люди, которые ранее состояли в браке, чаще отдают кредиты в срок, чем те, которые не были в браке.
Что касается дохода, можно придти к следующему выводу, что люди, чей доход свыше 200 тысяч в месяц, допускают куда меньше просрочек, чем люди, имеющие средний достаток (100-200 тысяч). Также, категория граждан, которая получает до 100 тысяч в месяц тоже зарекомендовали себя как ответственные плательщики.
 
 
