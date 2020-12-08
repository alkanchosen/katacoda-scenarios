## 1. Çalışma ortamınızı ayarlayın

Eğer Grafana'yı yerel makinenize kurmadan kullanmak istiyorsanız direkt Docker ile kullanabilirsiniz.

Grafana'yı plugin geliştirme için ayarlarken Docker kullanmak istiyorsanız aşağıdaki komutu çalıştırın:

```
docker run -d -p 3000:3000 -v "$(pwd)"/grafana-plugins:/var/lib/grafana/plugins --name=grafana grafana/grafana:7.0.0
```{{execute}}

Grafana'ya giriş yaparken username ve password girmeniz gerekmektedir. Bunlar varsayılan olarak şu şekildedir:

```
Email or username: admin
Password: admin
```

Grafana pluginleri sadece açılışta yüklediği için herhangi bir plugin eklediğinizde ya da kaldırdığınızda container'ı yeniden başlatmanız gerekmektedir.

```
docker restart grafana
```{{execute}}

Grafana'yı kullanmak için NodeJS 12 gerekmektedir. Hangi sürümün kurulu olduğunu `node -v`{{execute}} komutu ile öğrenebilirsiniz. Eğer mevcut sürüm 12 değilse
sürüm düşürmeniz gerekmektedir. Bu işlem için aşağıdaki adımları izleyin:

1. `sudo npm install -g n`{{execute}}

2. `sudo n 12`{{execute}}

**Sürüm düşürme işlemini yapmazsanız bir sonraki adımda hata alacaksınız.**
