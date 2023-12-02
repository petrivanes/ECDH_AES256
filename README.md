# ECDH_AES256
Simple ECDH and AES 256 implementation with OpenSSL
-- -- -- -- -- --
компиляция:
```sh
make all
```
===== error ===============
```text
в security.cpp
мелкие правки из-за ошибок

в main.cpp
ругалось на строки
```
```
ByteArray alice_msg_buffer(alice_msg.data(), alice_msg.length() + 1);
ByteArray bob_msg_buffer(bob_msg.data(), bob_msg.length() + 1);
```
ошибка:
```text
invalid conversion from ‘const void*’ to ‘void*’
```
поскольку:
alice_msg_buffer() принимает первым аргументом void*
а alice_msg.data() возвращает const char*

как вариант приводить типы с помощью
const_cast<тип>()
```
char* alice_msg_data = const_cast<char*>(alice_msg.data());
ByteArray alice_msg_buffer(alice_msg_data, alice_msg.length() + 1);
```
или проще:
```
ByteArray alice_msg_buffer(const_cast<char*>(alice_msg.data()), alice_msg.length() + 1);
...
ByteArray bob_msg_buffer(const_cast<char*>(bob_msg.data()), bob_msg.length() + 1);
```
=====  end error ========


