---
name: JoinBot
description: Понимание и использование JoinBot
---

![DALL·E – самурайский робот в красном лесу, 3D рендер](assets/cover.webp)

***ВНИМАНИЕ:** После ареста основателей кошелька Samourai и изъятия их серверов 24 апреля, **сервис JoinBot больше не доступен**. На данный момент использование этого инструмента невозможно. Однако вы все еще можете проводить Stonewall X2, но вам нужно найти партнера и вручную обменяться PSBT. Этот сервис может быть вновь запущен в ближайшие месяцы в зависимости от развития ситуации с делом.*

_Мы тщательно следим за развитием этого дела, а также за новостями, касающимися связанных с ним инструментов. Убедитесь, что мы обновим этот учебник, как только появится новая информация._

_Этот учебник предоставляется исключительно в образовательных и информационных целях. Мы не поддерживаем и не поощряем использование этих инструментов в преступных целях. Каждый пользователь несет ответственность за соблюдение законов в своей юрисдикции._

---

JoinBot – это новый инструмент, добавленный в набор Samourai Wallet с последним обновлением 0.99.98f известного программного обеспечения для биткойн-кошелька. Он позволяет легко совершать совместные транзакции для оптимизации вашей конфиденциальности, без необходимости искать партнера.

*Благодарим отличного Фаниса Михалакиса за идею использования DALL-E для миниатюры!*

## Что такое совместная транзакция в Bitcoin?

Bitcoin основан на распределенной и прозрачной бухгалтерской книге. Любой может отслеживать транзакции пользователей этой электронной денежной системы. Для обеспечения определенного уровня конфиденциальности пользователи Bitcoin могут совершать транзакции с определенной структурой, добавляя правдоподобное отрицание в их интерпретацию.

Идея не в том, чтобы напрямую скрыть информацию, а в том, чтобы запутать ее среди прочих. Эта цель используется в Coinjoins, транзакциях, которые разрывают историю монеты в Bitcoin и делают ее отслеживание сложным. Для достижения этого результата в транзакции должны быть созданы множественные входы и выходы одинаковой суммы.

Входы – это входы транзакции Bitcoin, а выходы представляют собой выходы. Транзакция использует свои входы для создания новых выходов, изменяя условия расходования монеты. Этот механизм позволяет перемещать биткойны между пользователями.
Об этом я подробно рассказываю в этой статье: Механизм транзакции Bitcoin: UTXO, входы и выходы.

Один из способов замаскировать следы в транзакции Bitcoin – совершить совместную транзакцию. Как следует из названия, это предполагает соглашение между несколькими пользователями, каждый из которых вносит сумму биткойнов в качестве входа в одну и ту же транзакцию и получает сумму в качестве выхода.

Как упоминалось ранее, наиболее известная структура совместной транзакции – Coinjoin. Например, в протоколе Coinjoin Whirlpool транзакции включают 5 участников как на входе, так и на выходе, каждый с одинаковым количеством биткойнов.

![Диаграмма транзакции Coinjoin на Whirlpool](assets/1.webp)

Внешний наблюдатель этой транзакции не сможет узнать, какой выход принадлежит какому пользователю на входе. Если взять пример пользователя №4 (фиолетовый), мы можем распознать их входной UTXO, но не узнаем, какой из 5 выходов на самом деле принадлежит им. Исходная информация не скрыта, а скорее запутана в группе.
Пользователь может отрицать владение определенным UTXO на выходе. Это явление называется "правдоподобное отрицание", и оно позволяет сохранить конфиденциальность в прозрачной транзакции Bitcoin.

Чтобы узнать больше о Coinjoin, я объясняю ВСЕ в этой длинной статье: Понимание и использование CoinJoin в Bitcoin.
Хотя Coinjoin очень эффективен для разрыва следа UTXO, он не подходит для прямых расходов. Действительно, его структура подразумевает использование входов предопределенного размера и выходов того же значения (с учетом комиссии за майнинг). Однако транзакция расходования на Bitcoin является критическим моментом для конфиденциальности, поскольку часто создает физическую связь между пользователем и его активностью в блокчейне. Поэтому кажется существенным использовать инструменты конфиденциальности для расходования. Существуют и другие коллаборативные структуры транзакций, специально разработанные для фактических платежных транзакций.
## Транзакция StonewallX2

Среди множества инструментов расходования, предлагаемых в кошельке Samourai Wallet, есть коллаборативная транзакция StonewallX2. Это мини Coinjoin между двумя пользователями, предназначенный для оплаты. Снаружи эта транзакция может привести к нескольким возможным толкованиям. Таким образом, она обеспечивает правдоподобное отрицание и, следовательно, конфиденциальность для пользователя.

Настройка коллаборативной транзакции StonewallX2 доступна в кошельках Samourai Wallet и Sparrow Wallet. Этот инструмент взаимодействует между двумя программами.

Его механизм довольно прост для понимания. Вот как это работает на практике:

> - Пользователь хочет совершить платеж в биткоинах (например, у торговца).
> - Он получает адрес получателя фактического платежа (торговца).
> - Он создает специфическую транзакцию с несколькими входами: по крайней мере один принадлежит ему и один принадлежит внешнему сотруднику.
> - Транзакция будет иметь 4 выхода, включая 2 одинаковых размера: один на адрес торговца для оплаты, один как сдача, возвращающаяся пользователю, один выход того же значения, что и платеж, идет сотруднику, и другой выход, который также возвращается сотруднику.

Например, вот типичная транзакция StonewallX2, в которой я совершил платеж на 50,125 сатоши. Первый вход на 102,588 сатоши поступает из моего кошелька Samourai. Второй вход на 104,255 сатоши поступает из кошелька моего сотрудника:

![Диаграмма транзакции StonewallX2](assets/2.webp)

Мы можем наблюдать 4 выхода, включая 2 одинаковых размера, чтобы запутать следы:

> - 50,125 сатоши, которые идут фактическому получателю моего платежа.
> - 52,306 сатоши, которые представляют мою сдачу и, следовательно, возвращаются на адрес в моем кошельке.
> - 50,125 сатоши, которые возвращаются моему сотруднику.
> - 53,973 сатоши, возвращающиеся моему сотруднику.
>   В конце операции сотрудник восстановит свой исходный баланс (за вычетом комиссии за майнинг), а пользователь оплатит покупку у торговца. Это добавляет значительное количество энтропии к транзакции и разрывает неоспоримые связи между отправителем и получателем платежа.

Сила транзакции StonewallX2 заключается в том, что она полностью нейтрализует одно из эмпирических правил, используемых аналитиками блокчейна: общее владение входами в мульти-входовой транзакции. Другими словами, в большинстве случаев, если мы наблюдаем биткоин-транзакцию с несколькими входами, мы можем предположить, что все эти входы принадлежат одному и тому же лицу. Сатоши Накамото уже указывал на эту проблему для конфиденциальности пользователей в своем Белом документе:

> "В качестве дополнительного барьера, для каждой транзакции можно использовать новую пару ключей, чтобы они не были связаны с общим владельцем. Однако связь неизбежна с мульти-входовыми транзакциями, которые неизбежно показывают, что их входы принадлежали одному и тому же владельцу."

Это одно из многих эмпирических правил, используемых в анализе блокчейна для построения кластеров адресов. Чтобы узнать больше об этих эвристиках, я рекомендую прочитать эту серию из четырех статей от Samourai, которая замечательно вводит в тему.
Сила транзакции StonewallX2 заключается в том, что внешний наблюдатель будет думать, что разные входы транзакции принадлежат одному владельцу. На самом деле это два разных пользователя, которые сотрудничают. Таким образом, анализ платежа вводится в заблуждение, и конфиденциальность пользователя сохраняется.
Снаружи транзакцию StonewallX2 невозможно отличить от транзакции Stonewall. Единственное реальное отличие между ними заключается в том, что Stonewall не является совместным. Она использует только UTXO одного пользователя. Однако в их структурах на учетной книге Stonewall и StonewallX2 идентичны. Это позволяет давать еще больше возможных толкований этой структуре транзакции, поскольку внешний наблюдатель не сможет определить, приходят ли входы от одного человека или от двух сотрудников.

Кроме того, преимущество StonewallX2 перед PayJoin типа Stowaway заключается в том, что его можно использовать в любой ситуации. Фактический получатель платежа не вносит никаких входов в транзакцию. Таким образом, StonewallX2 можно использовать для оплаты у любого продавца, принимающего Bitcoin, даже если продавец не использует Samourai или Sparrow.
С другой стороны, основным недостатком этой структуры транзакции является то, что она требует сотрудника, который готов использовать свои биткойны для участия в вашем платеже. Если у вас есть друзья, готовые помочь вам в любой ситуации, это не проблема. Однако, если вы не знаете других пользователей кошелька Samourai, или никто не доступен для сотрудничества, тогда вы застряли.

Для решения этой проблемы команда Samourai недавно добавила в свое приложение новую функцию: JoinBot.

# Что такое JoinBot?

Принцип работы JoinBot прост. Если вы не можете найти с кем сотрудничать для транзакции StonewallX2, вы можете сотрудничать с JoinBot. На практике вы будете проводить совместную транзакцию непосредственно с кошельком Samourai.

Эта услуга очень удобна, особенно для новичков, так как доступна 24/7. Если вам нужно совершить срочный платеж и вы хотите выполнить StonewallX2, вам больше не нужно связываться с другом или искать онлайн-сотрудника. JoinBot поможет вам.

Другое преимущество JoinBot заключается в том, что UTXO, которые он предоставляет в качестве входа, исключительно из постмикса Whirlpool, что улучшает конфиденциальность вашего платежа. Кроме того, поскольку JoinBot всегда в сети, вы должны сотрудничать с UTXO, которые имеют большой потенциальный Anonset.

Очевидно, у JoinBot есть некоторые компромиссы, которые следует отметить:

> Как и в случае с классическим StonewallX2, ваш сотрудник обязательно знает использованные UTXO и их назначение. В случае с JoinBot Samourai знает детали этой транзакции. Это не обязательно плохо, но это следует иметь в виду.
> Чтобы избежать спама, Samourai взимает сервисную плату в размере 3,5% от суммы фактической транзакции, с максимальным лимитом 0,01 BTC. Например, если я отправляю реальный платеж в 100 килосатоши с помощью JoinBot, сумма сервисного сбора составит 3 500 сатоши.
> Чтобы использовать JoinBot, у вас должно быть как минимум два несвязанных и доступных UTXO в вашем кошельке.
> В классическом StonewallX2 расходы на майнинг делятся поровну между двумя сотрудниками. С JoinBot, очевидно, вам придется платить полную сумму расходов на майнинг.
Для того чтобы транзакция JoinBot была точно такой же, как классическая транзакция StonewallX2 или Stonewall, оплата сервисных сборов производится в рамках совершенно отдельной транзакции. Возврат половины изначально уплаченных Samourai комиссий за майнинг будет осуществлен во время этой второй транзакции. Для оптимизации вашей конфиденциальности до конца, расчет комиссий выполняется с использованием структурированной транзакции Stowaway (PayJoin).

## Как использовать JoinBot?

Для выполнения транзакции JoinBot вам необходим кошелек Samourai. Вы можете скачать его здесь или в Google Playstore.

В отличие от большинства инструментов, разработанных Samourai, Sparrow Wallet пока не объявил о внедрении JoinBot. Таким образом, этот инструмент доступен только в Samourai.

Откройте пошаговую инструкцию по выполнению транзакции StonewallX2 с JoinBot в этом видео:

![Как использовать Joinbot](https://youtu.be/80MoMz2Ne5g)

Вот диаграмма транзакции, которую мы только что выполнили в видео:

![Диаграмма моей транзакции StonewallX2 с JoinBot.](assets/3.webp)

Мы видим 5 входов:

> - 3 входа по 100 килосатов от Samourai (JoinBot).
> - 2 входа из моего личного кошелька, по 3,524 сата и 1.8 мегасата.

Четыре выхода транзакции следующие:

> - 1 на 212,452 сата актуальному получателю моего платежа.
> - Еще один такой же суммы, который возвращается на адрес Samourai.
> - 1 сдача, которая также возвращается Samourai на 87,302 сата. Это представляет разницу между общим количеством их входов (300,000 сатов) и выходом для замешательства (212,452 сата) за вычетом комиссий за майнинг.
> - 1 сдача, которая возвращается на другой адрес в моем кошельке. Это представляет разницу между общим количеством моих входов и фактическим платежом за вычетом комиссий за майнинг.

Напоминаем, что комиссии за майнинг не представляют собой выходы транзакции. Они просто представляют разницу между общим количеством входов и общим количеством выходов.

## Заключение

JoinBot - это дополнительный инструмент, который добавляет больше выбора и свободы для пользователей Samourai. Он позволяет совершать совместную транзакцию StonewallX2 напрямую с Samourai в качестве сотрудника. Этот тип транзакции помогает улучшить конфиденциальность пользователя.

Если вы можете выполнить классическую транзакцию StonewallX2 с другом, я все же рекомендую использовать этот инструмент. Однако, если вы застряли и не можете найти сотрудников для совершения платежа, знайте, что JoinBot будет доступен 24/7 для сотрудничества с вами.

**Внешние ресурсы:**
- https://medium.com/oxt-research/understanding-bitcoin-privacy-with-oxt-part-1-4-8177a40a5923
- https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin