## 2. Yeni bir plugin oluşturun

Modern web geliştirme için araç geliştirmek zor olabilir. Kendi webpack konfigürasyonunuzu yazabilme imkanınız varken, bu rehber için, hazır bir şablon kullanacağız.

1. grafana-plugins klasörüne gidin.

```
cd grafana-plugins
``` {{execute}}

2. Şablonu `git clone` komutunu kullanarak oluşturun.
```
git clone https://github.com/grafana/grafana-starter-panel
``` {{execute}}

3. Gerekli bağımlılıkları yükleyin.
```
yarn install
``` {{execute}}

4. Plugini oluşturun.
```
yarn dev
``` {{execute}}

5. Grafana'nın yeni plugininizi keşfetmesi için Grafana sunucusunu yeniden başlatın.

```
docker restart grafana
``` {{execute}}

6. Grafana'yı açın ve **Configuration -> Plugins** kısmına gidin. Plugininizin `Grafana Panel Plugin Template` ismi ile orada olduğundan emin olun.

Grafana varsayılan olarak yeni bir plugin keşfettiğinde log dosyasına kayıt alır.
```
INFO[01-01|12:00:00] Registering plugin       logger=plugins name=my-plugin
```
