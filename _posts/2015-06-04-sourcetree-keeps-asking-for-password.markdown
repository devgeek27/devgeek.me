---
layout: post
title:  "Source Tree не запоминает пароль"
date:   2015-06-04 00:40:00
categories: software
tags: sourcetree, bitbucket, bug
---
Несколько недель назад, по какой-то неизвестной мне причине Source Tree перестал запоминать пароль для bitbucket аккаунта. Каждый раз при запуске Source Tree или спустя некоторое время после ввода пароля, Source Tree все равно спрашивал пароль. Каждый раз я ставил галочку Save to keychain, но это не помогало.

![Source Tree](/assets/article_images/2015-06-04-sourcetree-keeps-asking-for-password/s1.png)

Это очень мешало, так как пароль у меня сгенерированный и храниться в 1Password. Каждый раз, когда Source Tree спрашивал пароль, мне приходилось открывать 1Password, вводить мастер пароль, копировать пароль от bitbucket и вставлять его в Source Tree. Мне это надоело, и было решено это исправить. В логе Source Tree я нашел следующую строчку:

	Error (internetKeychainItemForServer:withUsername:path:port:protocol:) - The specified item could not be found in the keychain.
	
Судя по ошибке Source Tree не мог найти информацию для авторизации на bitbucket.org в Key Chain. Но она там была и легко находилась по поиску. Тогда я решил открыть свойства сохраненного пароля для bitbucket.org в Key Chain.

![Key Chain Access](/assets/article_images/2015-06-04-sourcetree-keeps-asking-for-password/s2.png)

Внимание мое привлекла вкладка Access Control, кликнув на которую все стало понятно. У Source Tree просто не было разрешения обращаться к этой информации. Добавив Source Tree в список программ, которые всегда имеют доступ к этой записи, я решил эту проблему.

![Key Chain Access](/assets/article_images/2015-06-04-sourcetree-keeps-asking-for-password/s3.png)