
## Требования к приложению "Кошелёк"

1. Приложение "Кошелёк" должно иметь установочный файл инсталятор для Windows, Linux, MacOS
2. Инсталятор должен/может быть представлен в виде одного-двух(-трёх файлов)
3. Инсталятор должен иметь лаконичный, понятный, дружелюбный для пользователя интерфейс
4. Установка/удаление приложения должна быть простой и прозрачной как для пользователя, так и для ОС:
	* Пользователь должен иметь возможность задавать путь к папке для установки
	* Пользователь должен иметь возможность легко удалить приложение из ОС со всеми служебными файлами

5. При первом запуске приложения должна быть предоставлена возможность (поле) для ввода секретного ключа пользователя, шифрующего БД с UTXO и инициализирующего генератор ключей
6. Приложение должно уведомлять пользователя о крайней степени важности знания секретного ключа в настоящее и будущее время
7. При запуске приложения должно быть поле для введения-идентификации секретного ключа пользователя
8. Приложение должно уведомлять пользователя о неверно введённом секретном ключе

9.  Приложение должно уметь показывать баланс пользователя
10. Приложение должно уметь отображать статистику статусов UTXO из БД 

11. Приложение должно уметь отображать статус соединения с другим "Кошельком"
12. Приложение должно уметь отображать этапы (в виде статусов) осуществления транзакции между двумя "Кошельками"
13. Приложение должно предоставлять понятный и дружелюбный интерфейс пользователю для:
	* связи с другим "Кошельком"
	* и осуществления транзакции

14. Приложение должно уведомлять пользователя:
	* о некорректной транзакции
	* о разрыве соединения с другим "Кошельком"

15. Приложение должно уметь показывать пользователю	историю его транзакциий совместно с историей изменения его баланса

## Вопросы
Приложение должно быть однопользовательским: один пользователь - одно приложение - один секретный ключ - одна БД для UTXO?

Или же приложение может быть многопользовательским: много пользователей - одно приложение - много ключей - несколько БД?




