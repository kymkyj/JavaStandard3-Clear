## mysql 패스워드 정책 권한 낮추기

 - mysql에서 처음에 policy 정책이 medium으로 되어있다.
 
정책 확인하는 명령어 : show variables like 'validate_password%';

mysql> show variables like 'validate_password%'; <br>
+--------------------------------------+--------+ <br>
| Variable_name                        | Value  | <br>
+--------------------------------------+--------+ <br>
| validate_password.check_user_name    | ON     | <br>
| validate_password.dictionary_file    |        | <br>
| validate_password.length             | 8      | <br>
| validate_password.mixed_case_count   | 1      | <br>
| validate_password.number_count       | 1      | <br>
| validate_password.policy             | MEDIUM | <br>
| validate_password.special_char_count | 1      | <br>
+--------------------------------------+--------+ <br>

- 명령어를 통해 나온 정책을 살펴보면
- validate_password.check_user_name : 패스워드에 user_id가 들어갔는지를 묻는 것
- length는 길이로 8자이상이어야한다는 뜻
- Mixed case count는 대소문자를 적어도 1회이상은 쓰란 말
- Number count도 숫자를 적어도 1회는 써야한다는 뜻
- Special char count는 특수문자를 적어도 1회이상은 써야한다는 뜻

정책 변경하는 명령어 : SET GLOBAL validate_password_policy=LOW; <- MEDIUM으로 변경도 가능

권한을 낮출때 에러가 발생한다
에러내용 : ERROR 1193 (HY000): Unknown system variable 'validate_password_policy'

- 정책에 대한것을 알수없는 값이다 라는 뜻 -> 즉 못찾는다.

아래의 명령어를 통해 위의 에러를 해결할 수 있다.

mysql> select plugin_name, plugin_status from information_schema.plugins where plugin_name like 'validate%';

mysql> install plugin validate_password soname 'validate_password.so';
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> select plugin_name, plugin_status from information_schema.plugins where plugin_name like 'validate%';
+-------------------+---------------+ <br> 
| plugin_name       | plugin_status | <br>
+-------------------+---------------+ <br>
| validate_password | ACTIVE        | <br>
+-------------------+---------------+ <br>
1 row in set (0.00 sec)

다시 정책을 변경해보면

mysql> set global validate_password_policy=LOW;
Query OK, 0 rows affected (0.00 sec)

성공뜬다.
