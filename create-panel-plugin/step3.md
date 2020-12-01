## 3. Pluginin yapısı

Pluginler farklı şekil ve büyüklüklerde gelir. Daha detaylı incelemeden önce hepsi tarafından kullanılan bazı dosyalara bakalım.

Oluşturduğunuz her plugin en az iki dosyaya ihtiyaç duyacak: `plugin.json` and `module.ts`.

### plugin.json

Grafana çalıştırıldığında plugin klasöründe `plugin.json` dosyası içeren bütün alt klasörleri tarar. `plugin.json` dosyası plugininiz hakkında bilgi içerir ve Grafana'ya plugininizin yapabildiklerini ve gerekli bağımlılıklarını iletir.

Bazı plugin tipleri farklı konfigürasyon seçeneklerine sahip olsa da zorunlu olanlara bakalım:

- `type` Grafana'ya plugininizin türünü söyler. Grafana üç farklı plugin türünü destekler: `panel`, `datasource` ve `app`.

- `name` kullanıcıların plugin listesinde göreceği isimdir. Eğer bir data source yaratıyorsanız bu genellikle bağlandığı veri tabanın ismini alır. Örnek: Prometheus, PostgreSQL, Stackdriver.

- `id` plugininizi özgün şekilde ifade eder ve diğer pluginlerle çakışmayı önlemek için Grafana kullanıcı adınızla başlamalıdır. Grafana kullanıcı adı almak için [Grafana'ya kaydolun](https://grafana.com/signup).

`plugin.json` dosyasındaki bütün konfigürasyon ayarlarına bakmak için [plugin.json şemasına](https://grafana.com/docs/grafana/latest/plugins/developing/plugin.json) bakın.

### module.ts

Grafana plugininizi keşfettikten sonra `module.ts` dosyasını yükler, bu dosya plugininizin giriş noktasıdır. `module.ts` plugininizin yazılımını içerir, bu yazılım oluşturduğunuz plugin tipine göre değişir.

Spesifik olarak `module.ts` [GrafanaPlugin'i](https://github.com/grafana/grafana/blob/08bf2a54523526a7f59f7c6a8dafaace79ab87db/packages/grafana-data/src/types/plugin.ts#L124) extend eden bir objeyi içermelidir. Bu aşağıdakilerden herhangi birisi olabilir:

* [PanelPlugin](https://github.com/grafana/grafana/blob/08bf2a54523526a7f59f7c6a8dafaace79ab87db/packages/grafana-data/src/types/panel.ts#L73)
* [DataSourcePlugin](https://github.com/grafana/grafana/blob/08bf2a54523526a7f59f7c6a8dafaace79ab87db/packages/grafana-data/src/types/datasource.ts#L33)
* [AppPlugin](https://github.com/grafana/grafana/blob/45b7de1910819ad0faa7a8aeac2481e675870ad9/packages/grafana-data/src/types/app.ts#L27)