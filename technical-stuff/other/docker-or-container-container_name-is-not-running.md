# Docker \| Container CONTAINER\_NAME is not running

أواجهة مشكلة مع _بعض_ نسخ Docker أنها حين توضع في وضع Daemon لا تظل تعمل

```text
docker run -d --name kali_apache kali_king-v1.04660a10a47d22a75f8d8d3cbba1c4731656fbf9ab76b641415b891a0419981b5
```

وبالتالي لا أستطيع أن أدخل علي سطر أوامرها لاحقا و عمل تعديلا عليها لحفظها

```text
docker exec -it kali_apache bash
Error response from daemon: Container kali_apache is not running
```

عند تتبع المشكلة باستخدام events

{% tabs %}
{% tab title="Command" %}
```text
docker events --filter container=kali_apache
```
{% endtab %}

{% tab title="Result" %}
```
2015-09-12T19:54:26.000000000+03:00 1989a4159c4c8bc92b80f075ac5d45c615a245bc959021c4b819941096bf9d1f: (from kali_king-v1.0) create
2015-09-12T19:54:26.000000000+03:00 1989a4159c4c8bc92b80f075ac5d45c615a245bc959021c4b819941096bf9d1f: (from kali_king-v1.0) start
2015-09-12T19:54:26.000000000+03:00 1989a4159c4c8bc92b80f075ac5d45c615a245bc959021c4b819941096bf9d1f: (from kali_king-v1.0) die
```
{% endtab %}
{% endtabs %}

وجدت أنه يتم إنشاء الـ Container وتشغيله ثم إغلاقه بدون أي تدخل مني في إغلاقه. هذه المشكلة بسبب إعادات الـ image نفسها من ملف DockerFile

لحل هذه المشكلة جعل كالي تشغل مع Process دائمة ك daemon

أجعل النسخة تنظر مدة كافية لعمل ما تريد مثلا 1000 ثانية

```text
docker run -d -it --name kali_apache kali_king-v1.0 bash
```

الأن دخل إلى ال container وانجز عملك كما تشاء

```text
docker exec -it kali_apache bash
```

