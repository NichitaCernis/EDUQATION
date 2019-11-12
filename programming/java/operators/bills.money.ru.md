## Типы, операции, преобразование

> В программировании часто применяется принцип, называемый «аккумулятор / накопитель», чаще всего так называется переменной, которая запоминает промежуточное значение пока в программе есть последовательные операции которым необходимо это значение. Например, если бы мы хотели, чтобы в **money_accumulator** собирали сумму денег у 3 человек последовательно (пошагово), а затем тратили бы деньги из накопившейся суммы, в коде это выглядело бы так:

```java
int money_1 = 100;
int money_2 = 200;
int money_3 = 300;

int money_accumulator = 0;

int expenses = 45;

money_accumulator = money_accumulator + money_1;
money_accumulator = money_accumulator + money_2;
money_accumulator = money_accumulator + money_3;

money_accumulator = money_accumulator - expenses;

```

---

* Требуется улучшить код так чтобы с одной стороны НЕ НАРУШИТЬ последовательность и логику, с другой стороны чтобы он стал КОМПАКТНЕЕ!
* Требуется улучшить качество кода (конвенции наименования)
* ТАК ЖЕ требуется вывести на экране СХЕМУ "операций" кода в таком формате:
  ``` 
      555MDL:
      100MDL
    + 200MDL
    + 300MDL
    -------- 
    - 45MDL 
  ```
<details>
    <summary>Подсказка?</summary>

   в тексте (String - "то что в ковычках") в Java есть некоторые "специальные символы":
   * \t	Символ табуляции.
   * \b	Символ возврата в тексте на один шаг назад ил уаление одного символа в строке (backspace).
   * \n	Символ перехода на новую строку.
   * \r	Символ возврата каретки.
   * \f	Прогон страницы.
   * \'	Символ одинарной кавычки.
   * \"	Символ двойной кавычки.
   * \\	Символ обратной косой черты (\).
</details>