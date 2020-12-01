## 4. Panel Pluginleri

Grafana 6.x'ten beri paneller ReactJS [bileşen sınıflarıdır](https://reactjs.org/docs/components-and-props.html). (component)

Grafana 6.0'dan önce pluginler [AngularJS](https://angular.io/) ile yazılmıştı. AngularJS ile yazılan pluginleri hala desteklememize rağmen yeni pluginleri ReactJS ile yazmanızı şiddetle öneriyoruz.

### Panel özellikleri

[PanelProps](https://github.com/grafana/grafana/blob/747b546c260f9a448e2cb56319f796d0301f4bb9/packages/grafana-data/src/types/panel.ts#L27-L40) arayüzü (interface) panel boyutları, zaman aralığı gibi panel bilgileri içerir. 

Panel özelliklerine `props` aracılığıyla ulaşabilirsiniz.

**src/SimplePanel.tsx**

```javascript
const { options, data, width, height } = props;
```

### Geliştirme akışı

Şimdi panelinize değişiklik yapmayı, paneli oluşturmayı ve Grafana'yı yeniden başlatmayı içeren bir akış öğreneceksiniz.

Önce panelinizi dashboard'a eklemeniz gerekmektedir:

1. Grafana'yı tarayıcınızda açın.
2. Yeni bir dashboard oluşturun ve yeni bir panel ekleyin.
3. Görselleştirme tiplerinden sizin panelinizi seçin.
4. Dashboard'u kaydedin.

Şimdi panelinizi gördüğünüze göre panel plugininde değişiklik yapmayı deneyin:

1. `SimplePanel.tsx` dosyasında çemberin `fill` rengini değiştirin.
2. Plugini oluşturmak için `yarn dev` komutunu çalıştırın.
3. Yeni değişikleri görmek için tarayıcınızda Grafana'yı tekrardan çalıştırın.