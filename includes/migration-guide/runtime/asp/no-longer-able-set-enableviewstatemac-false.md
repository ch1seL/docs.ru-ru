### <a name="no-longer-able-to-set-enableviewstatemac-to-false"></a>Свойству EnableViewStateMac больше невозможно задавать значение false

|   |   |
|---|---|
|Подробные сведения|ASP.NET теперь не позволяет разработчикам указывать <code>&lt;pages enableViewStateMac=&quot;false&quot;/&gt;</code> или <code>&lt;@Page EnableViewStateMac=&quot;false&quot; %&gt;</code>. Код проверки подлинности сообщения (MAC) состояния просмотра теперь принудительно применяется для всех запросов со встроенным состоянием просмотра. Затрагиваются только те приложения, в которых для свойства EnableViewStateMac явно задано значение <code>false</code>.|
|Предложение|Следует считать, что свойство EnableViewStateMac имеет значение true, и возникающие ошибки MAC должны быть устранены (как описано в [этом](https://support.microsoft.com/kb/2915218) руководстве, содержащем несколько решений в зависимости от причины ошибки MAC).|
|Область|Значительно|
|Версия|4.5.2|
|Тип|Среда выполнения|
