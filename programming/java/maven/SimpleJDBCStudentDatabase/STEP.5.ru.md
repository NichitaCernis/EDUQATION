### Update репозитория данных и модели данных

1. в класс Student добавить свойство "private Integer id". Теперь когда вы будете сохранять в базу студентов, объект студента создаем так ```new Student( null, "Full Name", ... )``` так как до сохранения мы не знаем какой у него "id" - ставим null, а вот когда студента ЧИТАЮТ из базы ```new Student( rs.getInt("id"), rs.getString("fullname"), ... )```
2. в класс StudentRepository добавить еще метод "update( Student student )" который должен запустить в базу такой запрос:
   ```sql
   UPDATE students SET fullname = '???', dob='???', .... WHERE id = ???;
   ``` 
 тоесть чтобы одновнить инфу студента, надо чтобы мы знали его "id", в данном случае все "???" берутся из полей переданного методу объекта "student"   
3. в класс StudentRepository добавить еще метод "delete( Student student )" который должен запустить в базу такой запрос:
   ```sql
   DELETE FROM students WHERE id = ???;
   ``` 
 тоесть чтобы удалить студента, надо чтобы мы знали его "id", в данном случае "???" берется из полей переданного методу объекта "student"   