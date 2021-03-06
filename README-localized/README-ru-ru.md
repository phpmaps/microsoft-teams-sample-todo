---
page_type: sample
products:
- office-teams
- office-outlook
- office-365
languages:
- typescript
- nodejs
extensions:
  contentType: samples
  technologies:
  - Tabs
  createdDate: 10/19/2016 12:06:51 PM
---
# Пример приложения со вкладками "Список дел" для Microsoft Teams
[![Состояние сборки](https://travis-ci.org/OfficeDev/microsoft-teams-sample-todo.svg?branch=master)](https://travis-ci.org/OfficeDev/microsoft-teams-sample-todo)

Это пример [приложении "Вкладка" для Microsoft Teams](https://aka.ms/microsoftteamstabsplatform). Он призван показать, как легко преобразовать имеющееся веб-приложение в приложение Microsoft Teams со вкладками. Существующее веб-приложение [**TodoMVC для React**](https://github.com/tastejs/todomvc/tree/gh-pages/examples/typescript-react)— это основной диспетчер задач, который интегрируется с вашими личными задачами Outlook. С помощью всего лишь нескольких незначительных изменений этот веб-вид можно добавить в канал в качестве приложения с вкладками. Обратите внимание на [различие между ветвями "до" и "после"](https://github.com/OfficeDev/microsoft-teams-sample-todo/compare/before...after), чтобы увидеть, какие изменения были сделаны.

> **Примечание.** Это не реалистичный пример приложения для совместной работы. Показанные задачи принадлежат индивидуальной учетной записи пользователя, а не общей учетной записи группы.

**Для получения дополнительной информации о разработке приложений для Microsoft Teams, пожалуйста, просмотрите [документацию для разработчиков](https://msdn.microsoft.com/en-us/microsoft-teams/index) Microsoft Teams.**

## Необходимые компоненты

1. [Учетная запись Office 365 с доступом к командам Microsoft.](https://msdn.microsoft.com/en-us/microsoft-teams/setup).
2. Этот образец построен с использованием [Node.js](https://nodejs.org). Загрузите и установите рекомендуемую версию, если у вас ее еще нет.

## Запуск приложения

### Разместите вкладку приложения «Страница конфигурации» и «Страница содержимого»

Поскольку страницы конфигурации вкладок и содержимого являются веб-приложениями, они должны быть размещены.  

Сначала мы подготовим проект:

1. Клонируйте репозиторий.
2. Откройте командную строку в подпапке "репозиторий".
3. В командной строке запустите `npm installl` (входит в состав узла Node. js).

Чтобы разместить приложение локально:
* В подкаталоге repo запустите `npm start`, чтобы запустить `webpack-dev-server`, чтобы включить приложение dev.
* Обратите внимание, что манифест dev настроен на использование localhost, поэтому дополнительная настройка не требуется.

При желании можно создать развертываемое приложение, которое вы можете разместить в собственной среде:
* В подкаталоге repo запустите `npm run build`, чтобы создать развертываемую сборку.
* Измените config.url в манифесте prod, чтобы указать местоположение вашего хостинга. [См. ниже](#registering-an-application-to-authenticate-with-microsoft)

### Добавьте вкладку в Microsoft Teams

1. Скачайте на вкладку [ пакет разработки для приложения ](https://github.com/OfficeDev/microsoft-teams-sample-todo/tree/master/package/todo.dev.zip) ZIP-файл".
2. При необходимости создайте новую группу для тестирования. В нижней части левой панели щелкните **создание группы**.
3. Выберите команду на левой панели, выберите **... (дополнительные параметры)**, а затем выберите **Просмотр команды**.
4. Откройте вкладку **разработчик (Предварительная версия)**, а затем выберите **загрузить**.
5. Перейдите к загруженному zip-файлу из шага 1 выше и выберите его.
6. Перейти на любой канал в команде. Щелкните знак "+" справа от существующих вкладок.
7. Выберите вкладку в галерее, которая появляется.
8. Примите запрос на согласие.
9. При необходимости войдите в систему, используя свою служебную / учебную учетную запись Office 365. Обратите внимание, что код попытается выполнить тихую аутентификацию, если это возможно.
10. Проверьте информацию аутентификации.
11. Чтобы добавить вкладку на канал, нажмите кнопку Сохранить.

> **Примечание.** Чтобы повторно загрузить обновленный пакет с тем же `идентификатором`, щелкните значок «Заменить» в конце строки таблицы вкладки. Не нажимайте кнопку "Отправить" снова. Microsoft Teams скажет, что вкладка уже существует.

> Желательно иметь несколько конфигов, по одному на среду. Имена zip-файлов могут быть любыми, такими как `todo.dev.zip`, `todo.prod.zip` и т. Д., Но zip-файл должен содержать `manifest.json` с уникальным `идентификатором`. Дополнительные сведения см. в статье [создании манифеста для вкладки](https://msdn.microsoft.com/en-us/microsoft-teams/createpackage).

## Пошаговое руководство по кодированию

В то время как `основная` ветвь показывает последнее состояние образца, взгляните на следующие [различия кода](https://github.com/OfficeDev/microsoft-teams-sample-todo/compare/before...after) между:

* [`перед`](https://github.com/OfficeDev/microsoft-teams-sample-todo/commit/before): исходное приложение

* [`после`](https://github.com/OfficeDev/microsoft-teams-sample-todo/commit/after): это приложение после интеграции с Microsoft Teams.

Проходя этот шаг за шагом:

1. Мы добавили новую `config.html` и `config.tsx` страницы, которая отвечает за то, чтобы пользователь имел возможность манипулировать параметрами, сигнон проверку подлинности на основе одного и того же. во время первого запуска. Это необходимо для того, чтобы администратор группы мог настроить приложение / параметры. Дополнительные сведения см. в статье [создание страницы настройки](https://msdn.microsoft.com/en-us/microsoft-teams/createconfigpage).

2. Мы добавили тот же файл `config.html` в нашу конфигурацию `webpack.common.js`, чтобы он мог вводить правильные пакеты во время выполнения.

3. Мы добавили ссылку на `MicrosoftTeams.js` в наш index.html и добавили `MicrosoftTeams.d.ts` для IntelliSense Typescript.

4. Мы добавили `manifest.dev.json`, `manifest.prod.json` и два логотипа для размера *44x44* и *88x88*. Не забудьте переименовать их как `manifest.json` в ZIP-файлах, которые вы отправите в Microsoft Teams.

5. Мы добавили стили в нашу `app.css`.

6. Наконец, мы изменили `аутентификацию` в outlook.tasks.ts, чтобы вместо нее использовать «useMicrosoftTeamsAuth», новую функцию из бета-версии OfficeHelpers, на которую ссылается этот пример.

### Вызов диалога аутентификации

Когда пользователь добавляет вкладку, отображается страница конфигурации (config.html). В этом случае код аутентифицирует пользователя, если это возможно.

Аутентификация использует новую функцию, специфичную для команд, в последней (> 0.4.0) версии библиотеки [office-js-helpers](https://github.com/OfficeDev/office-js-helpers). Эта вспомогательная функция попытается выполнить автоматическую аутентификацию, но если она не сможет, она вызовет специальный диалог авторизации Microsoft Teams. Дополнительные сведения о процессе полной проверки подлинности в Microsoft Teams см. в статье [проверка подлинности пользователя](https://msdn.microsoft.com/en-us/microsoft-teams/auth) в[документации для разработчиков](https://msdn.microsoft.com/en-us/microsoft-teams/index) Microsoft Teams.

В outlook.tasks.ts:
```typescript
 return this.authenticator.authenticate('Microsoft')
    .then(token => this._token = token)
    .catch(error => {
        Utilities.log(error);
        throw new Error('Failed to login using your Microsoft Account');
    });
```

### Обработка события «Сохранить»

После успешного входа пользователь сохранит вкладку в канал. Следующий код включает кнопку «Сохранить» и устанавливает SaveHandler, который будет хранить то, что контент будет отображаться на вкладке (в данном случае, только index.html проекта).

In config.tsx:
```typescript
    initialize({ groupId, upn}) {
        this.setState({ groupId, upn });
        console.log(this.state);
        /** Enable the Save button  */
        microsoftTeams.settings.setValidityState(true);
        /** Register the save handler */
        microsoftTeams.settings.registerOnSaveHandler(saveEvent => {
            /** Store Tab content settings */
            microsoftTeams.settings.setSettings({
                contentUrl: `${location.origin}/index.html`,
                suggestedDisplayName: "My Tasks",
                websiteUrl: `${location.origin}/index.html`
            });
            saveEvent.notifySuccess();
        });
    }
```

## Используемая технология

В этом примере используется следующий стек:

1. [`React от Facebook`](https://facebook.github.io/react/) как UI Framework.
2. [`TypeScript`](https://www.typescriptlang.org/) как транспортер.
4. [`TodoMVC`](http://todomvc.com/examples/typescript-react/#/) основа для функциональности TodoMVC.
5. [`Webpack`](https://webpack.github.io/) как инструмент сборки.

## Дополнительные ресурсы

### Регистрация приложения для аутентификации в Microsoft
Обратите внимание, что в этом нет необходимости, если вы используете выше локальную опцию Dev, но если вы решите разместить эту вкладку в своей среде, вы должны зарегистрировать приложение для аутентификации.

1. Перейдите на [портал регистрации приложений (Майкрософт)](https://apps.dev.microsoft.com).
2. Войдите в свою учетную запись Office 365 для работы / школы. Не используйте свою личную учетную запись Microsoft.
2. Добавление нового приложения.
2. Запишите ваш новый `идентификатор приложения`.
2. Нажмите кнопку `добавить платформу` и выберите `веб`.
3. Установите флажок `Разрешить неявный поток` и настройте URL-адрес перенаправления следующим образом: `https://<mywebsite> /config.html`.

Для получения дополнительной информации о размещении собственных вкладок см. [Образец README для команд Microsoft «Начало работы»](https://github.com/OfficeDev/microsoft-teams-sample-get-started#host-tab-pages-over-https).

>**Примечание.** По умолчанию ваша организация должна позволять вам создавать новые приложения. Но если этого не произойдет, вы можете получить тестового арендатора для разработчиков, бесплатную годовую пробную подписку на Office 365 для разработчиков. [Вот как](https://msdn.microsoft.com/en-us/microsoft-teams/setup).


## Сведения об авторах

Этот проект основан на Typescript TodoMVC - шаблон React, расположенный [здесь](https://github.com/tastejs/todomvc/tree/gh-pages/examples/typescript-react).

## Участие

Пожалуйста, ознакомьтесь с разделом [Участие](contributing.md) для получения подробной информации о нашем кодексе поведения и процедуре отправки нам запросов на выдачу.

Этот проект соответствует [Правилам поведения разработчиков открытого кода Майкрософт](https://opensource.microsoft.com/codeofconduct/). Дополнительные сведения см. в разделе [часто задаваемых вопросов о правилах поведения](https://opensource.microsoft.com/codeofconduct/faq/). Если у вас возникли вопросы или замечания, напишите нам по адресу [opencode@microsoft.com](mailto:opencode@microsoft.com).

## Управление версиями

Чтобы использовать управление версиями, мы используем[SemVer](http://semver.org/). Чтобы узнать, какие версии доступны, см. [Теги в этом репозитории](https://github.com/officedev/microsoft-teams-sample-todo/tags).

## Лицензия

Этот проект лицензируется по лицензии MIT - подробности см. В файле [лицензии](LICENSE).
