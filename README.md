# <a name="up" />Проект Яндекс Самокат

Яндекс Самокат — позволяет пользователям заранее зазазать на домой самокаты на определенное время и место. Пользователи получают гарантированную доступность, уведомления, и могут гибко управлять заказами через веб-приложение.

## Содержание
- [Задачи тестировщика](#задачи-тестировщика)
- [Требования по проекту](#требования-по-проекту)
- [Инструменты](#инструменты)
- [Проектирование тестовой документации](#проектирование-тестовой-документации)
- [Выполнение тестов](#выполнение-тестов)

## Задачи тестировщика

<details>
<summary> 1-спринт </summary> 

1. Проанализировать требования к веб-приложению Яндекс Самокат
2. Разработать mindmap функциональности формы заказа (логика работы и вёрстка)
3. Составить чек-лист по требованиям к функциональности экрана «Статус заказа»
4. Для экрана «Сделать заказ» составить проверки на валидацию полей
5. Провести тестирование и формить баг-репорты
6. +Провести тестирование всей функциональности по макетам и требованиям

***

</details>

## Требования

<details>
<summary> Требования к веб-приложению </summary> 

### Поддерживаемые окружения  
Приложение поддерживает эти браузеры: Яндекс.Браузер не ниже версии 20.0.1, Chrome не ниже версии 85. Будет поддерживаться разрешение экрана 1280x720 и 1920x1080.  

### Лендинг
Есть заголовок и чертёж самоката. При скролле происходит анимация: чертёж сменяется фотографией, появляется таблица с описанием самоката.  
В шапке лендинга есть две кнопки: «Заказать», «Статус заказа».   
Появляется запрос на согласие использовать куки.   
Если доскроллить до третьего блока, появляется информация: «Как это работает», «Вопросы о важном».  

#### Экран «Сделать заказ»  
Чтобы сделать заказ, нужно заполнить две формы: «Для кого самокат», «Про аренду».  

**Для кого самокат**
Поля: «Имя», «Фамилия», «Адрес: куда привезти самокат», «Станция метро», «Телефон: на него позвонит курьер».  
Все поля обязательные. Если они не заполнены корректно, нельзя перейти на следующую страницу.  
Внизу кнопка «Дальше»: она переводит на форму «Про аренду».   

**Про аренду**
Поля: «Когда привезти самокат», «Срок аренды», «Цвет», «Комментарий».   
«Когда привезти самокат», «Срок аренды» — обязательные поля.   
«Цвет», «Комментарий» — необязательные.  

**Кнопка «Назад».** При нажатии пользователь переходит на страницу «Для кого самокат».  При переключении между страницами введённая информация сохраняется.  

**Кнопка «Заказать».** Если все поля заполнены корректно, при клике по кнопке «Заказать» заказ будет оформлен. Появится всплывающее окно с текстом «Номер заказа NNNNN.   Запишите его: пригодится, чтобы отслеживать статус» и кнопкой «Посмотреть статус». Кнопка «Посмотреть статус» ведёт на экран «Статус заказа»: в нём уже заполнено поле «Номер заказа».  
Если не все обязательные поля заполнены корректно, при нажатии на кнопку «Заказать» появится ошибка «Введите корректный <имя поля>»  
Пользователь может сделать несколько заказов один за другим.  

#### Экран «Статус заказа»
Если нажать на «Статус заказа» в шапке лендинга, появляется поле ввода «Номер заказа». Нужно ввести значение и нажать Enter. Если номер заказа введён корректно, появляется информация:  
- Данные заказа пользователя: имя, фамилия, адрес и остальные. Для всех полей действует правило: если текст не умещается в одной строке, он переносится на вторую.  
- Цепочка статусов заказа. Текущий статус выделен чёрным, остальные — серые. Если статус пройден, цифра перед ним сменяется на галочку.  
Если номер заказа введён некорректно, появляется сообщение об ошибке: «Такого заказа нет. Точно верный номер?».  
На экране статуса заказа четыре статуса. Активным может быть только один из них — он показывает, на какой стадии находится заказ:     
- **«Самокат на складе»**. Становится активным, когда пользователь сделал заказ.  
- **«Курьер едет к вам»**. Становится активным, когда курьер подтвердил у себя в приложении, что принял заказ. Когда статус активен, в подписи появляется имя курьера: «Курьер Фродо едет к вам». Если имя курьера слишком длинное и подпись не умещается в одну строчку, текст переносится на вторую строчку.  
- **«Курьер на месте»**. Становится активным, когда курьер нажал кнопку «Завершить» у себя в приложении.  
- **«Ну всё, теперь кататься»**. Становится активным, когда курьер подтвердил завершение заказа. Под заголовком статуса подпись «Аренда закончится...». Показываемое время рассчитывается от момента, когда самокат передали пользователю с учётом количества дней. Когда время аренды заканчивается, статус меняется на «Время аренды кончилось» с подписью «Скоро курьер заберёт самокат».  
Пользователь может ввести номер другого заказа и посмотреть его статус.  

**Отмена заказа**
Есть кнопка «Отменить заказ». Если кликнуть по ней, появится всплывающее окно с текстом «Хотите отменить заказ?» На всплывающем окне две кнопки: «Отменить», «Назад». 
Если кликнуть по «Назад», пользователь вернётся на страницу статуса заказа.   
Если кликнуть по «Отменить», появится всплывающее окно с текстом «Заказ отменён. Возвращайтесь, мы всегда вас ждём :)» и кнопкой «Хорошо». Кнопка «Хорошо» ведёт на главную страницу лендинга.  
Пользователь может отменить заказ, пока курьер не взял его в работу. Когда заказ уже у курьера, кнопка «Отменить заказ» будет некликабельной.  
Отменённый заказ удаляется из системы. Пользователь не может его посмотреть.  

**Просроченный заказ**
Заказ считается просроченным, если курьер не успел выполнить его вовремя. Например, пользователь заказал самокат на 1 января. Если 1 января самокат не доставлен до 23:59, этот заказ — просроченный.  
Если заказ просрочен, его статус меняется на «Курьер задерживается», а подпись — на «Не успеем привезти самокат вовремя. Чтобы уточнить статус заказа, позвоните в поддержку: 0101». Статус и подпись подсвечиваются красным.  
Если пользователю доставили просроченный заказ, отсчёт времени до конца аренды начинается с момента получения заказа.  

### Доработка фронтенда
В цепочку статусов добавлен пятый статус: «Время аренды кончилось»**.** Это фича, которую реализовали только во фронтенде, и бэкенд ещё не готов. ****Раньше этот текст появлялся на месте четвёртого статуса — в момент, когда время аренды заканчивалось. Теперь текст в четвёртом статусе не меняется: он просто становится серым, как и остальные статусы.  
Пример ответа описан в документации к API в блоке *Orders — Получить заказ по его номеру.*  
Номер нового статуса в запросе = 3.  

![iScreen Shoter - Safari - 231110182709](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/54c9deb5-212d-49f0-849d-ea96e193f38a)

### FAQ

**Сколько это стоит? И как оплатить?**  
Сутки — 400 рублей. Оплата курьеру — наличными или картой.  

**Вы привозите зарядку вместе с самокатом?**  
Самокат приезжает к вам с полной зарядкой. Этого хватит на восемь суток — даже если будете кататься без передышек и во сне. Зарядка не понадобится.  

**Сможете привезти самокат прямо сегодня?**  
Только начиная с завтрашнего дня. Но скоро станем расторопнее.  

**Хочу сразу несколько самокатов! Так можно?**  
Пока что так: один заказ — один самокат. Если хотите покататься с друзьями, можете просто сделать несколько заказов.  

**Можно ли продлить заказ или вернуть самокат раньше?**  
Пока что нет! Если что-то срочное — всегда можно позвонить в поддержку по номеру 0101.  

**Можно ли отменить заказ?**  
Да, отменить можно, пока курьер не выдвинулся к вам с самокатом. Штрафа не будет, объяснительной записки не попросим.  

**Как рассчитывается время аренды?**  
Допустим, вы оформляете заказ на 8 мая. Мы привозим самокат в эту дату до конца дня. Отсчёт времени аренды начинается с момента, когда вы оплатите заказ курьеру. Если мы привезли самокат 8 мая в 20:30, суточная аренда закончится 9 мая в 20:30.  

**Я живу за МКАДом, привезёте?**  
Да, обязательно. Всем самокатов! И Москве, и Московской области.  

***

</details>

<details>
<summary> Макеты к веб-приложению </summary> 
   
- [Main](#main)
- [Flow statuses](#flow-statuses)
- [UI KIT](#ui-kit)

## Main
### Main page 1280
![web_page-0001](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/7537caaa-7728-4177-8523-705bf083b1f6)

### Form about customer
![web_page-0002](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/f1d9d4e2-0673-4a12-8716-c0653dd4d4d5)

### Search order number
![web_page-0003](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/e44fa48d-c65e-4563-b993-21ef1d447997)

### Form about customer (full)
![web_page-0006](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/d76104d9-0e5d-457b-8b79-a490c0261b14)

### Form about rent
![web_page-0010](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/07b72881-fe44-4c65-9542-a6ddec349ecb)

### Form about rent (full)
![web_page-0011](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/1c015f11-7686-46d9-b1c2-18baf2912437)

### Popap successful order
![web_page-0015](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/ab38c71c-458b-4683-ab1a-a3f2218a38f9)

### Order status full
![web_page-0004](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/1529968e-f52d-43b8-8aba-1e7605164ff8)

### Cancel order
![web_page-0007](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/2967f7dc-4de6-4a04-9d4c-96703a36d7ac)

### Successful cancel order
![web_page-0012](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/c0a85026-818e-4024-a473-7968d4c7297c)

### 404 error
![web_page-0005](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/af5668ef-461b-4ec4-89bf-5b1b2d6c4159)

### Main page 1920
![web_page-0013](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/a114a3d5-c31f-4c79-bf0c-74dc85689d5d)

### Form about customer
![web_page-0008](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/54939334-9e8f-4cec-83cb-8f435a954fce)

### Order status full
![web_page-0009](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/b51f5283-5e59-471b-8d21-aafee230b0bf)

### Cancel order
![web_page-0014](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/97da3ca7-1613-4086-b28f-522af95b46d8)

### Successful cancel order
![web_page-0017](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/e65d933e-5f4c-4518-8650-0547058e7416)


## Flow statuses
### Order is late
![web_page-0016](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/d40b07d3-5e31-4a75-86da-13f45aa6dfd8)

### Status active 1
![web_page-0018](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/ba2bc369-4e21-490f-93b3-6df8431ef75e)

### Status active 2
![web_page-0019](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/76878702-110a-480c-8af9-5f15d16f54ed)

### Status active 3
![web_page-0026](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/116b285c-ba31-4374-acc6-5ad5e368da5d)

### Status active 4
![web_page-0025](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/f4b366d6-5976-47fc-8a68-7ef0243196a7)

### Status active 4+
![web_page-0029](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/e019f822-0471-4cea-8d59-910aa6668fe6)

### Status active 5
![web_page-0030](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/b4005586-1b64-4402-bd36-e97ce15bb579)

## UI KIT
### Flow button
![web_page-0020](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/aecd2498-170d-43b6-ab0c-969ff557e5b3)

### Flow faq
![web_page-0021](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/b1898dac-7aaa-4a78-bed5-cd71fb7e0312)

### Cookie
![web_page-0023](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/1c639581-a307-4d80-9298-9b2162cdeeaa)

### Flow input
![web_page-0022](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/ab7ce71f-12f6-41e5-8728-104bdd0c366c)

### Flow unerground
![web_page-0024](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/174cdb07-8ba3-46ef-aa02-82a69ca83e57)

### Flow date
![web_page-0027](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/54c2d6a1-b637-430b-a14e-e03e981487a8)

### Flow rental period
![web_page-0028](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/58109e05-4342-484a-9f75-d5b3c78f9596)

### Flow color
![web_page-0031](https://github.com/SofiiaSleptsova/Samokat_Yandex/assets/147629405/4c8e2ad1-5c4d-4558-b4a7-0e91e62d6942)































***

</details>

## Инструменты
<p align="left"> 
   <a href="https://miro.com/" target="_blank" rel="noreferrer"><img src="https://w7.pngwing.com/pngs/885/629/png-transparent-miro-hd-logo-thumbnail.png" width="36" height="36" alt="Miro" /></a>
   <a href="https://www.figma.com/" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/figma-colored.svg" width="36" height="36" alt="Figma" /></a>
  <a href="https://docs.google.com/" target="_blank" rel="noreferrer"><img src="https://w7.pngwing.com/pngs/240/1015/png-transparent-g-suite-google-docs-google-angle-rectangle-logo.png" width="36" height="36" alt="Google Sheets" /></a>
  <a href="https://www.jetbrains.com/youtrack/" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/9/95/YouTrack_Icon.png" width="36" height="36" alt="Youtrack" /></a>
  <a href="https://developer.android.com/studio" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c1/Android_Studio_icon_%282023%29.svg/800px-Android_Studio_icon_%282023%29.svg.png" width="36" height="36" alt="Android_Studio" /></a>
   <a><img src="https://d33wubrfki0l68.cloudfront.net/38b5c953a4667366685d55db55d057c86db1fc54/a0fdc/static/acae6b24d940347661ca901ea07f47c1/chrome-dev-logo-icon.png" width="36" height="36" alt="Devtools" /></a>
  <a href="https://www.postman.com/" target="_blank" rel="noreferrer"><img src="https://seeklogo.com/images/P/postman-logo-0087CA0D15-seeklogo.com.png" title="postman" width="36" height="36" alt="Postman" /></a>
  <a href="https://www.charlesproxy.com/" target="_blank" rel="noreferrer"><img src="https://davidwalsh.name/demo/charlesproxyicon.svg" width="36" height="36" alt="Charles" /></a>
  <a href="https://www.postgresql.org/" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/postgresql-colored.svg" width="36" height="36" alt="PostgreSQL" /></a>
</p> 
