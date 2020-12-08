## 6. Data frame'leri kullanarak dinamik paneller yaratın

Çoğu panel Grafana data source'dan gelen dinamik veriyi görselleştirir. Bu adımda, her bir serideki sayıyı kullanarak için yarıçapı bu sayı olan yeni çemberler yaratacaksınız.

> Panelinizde veri tabanından gelen verileri kullanmak için data source kurmanız gerekmektedir. 
> Eğer mevcut bir tane yoksa, geçici olarak [TestData DB'i](https://grafana.com/docs/grafana/latest/features/datasources/testdata) kullanabilirsiniz.

Data source'dan gelen veriler panel bileşen sınıfının (component) içindeki `data` değişkeninde bulunur.

```typescript
const { data } = props;
```

`data.series` data source'dan gelen serileri içerir. Her bir seri *data frame* denilen bir veri yapısı şeklinde gösterilir. *Data frame* gelen verileri sütunlara koyup yeni bir tablo oluşturur. Her bir sütundaki veri aynı veri yapısındadır: string, int veya time. 

Aşağıda `Time` ve `Value` sütununa sahip örnek bir *data frame* görebilirsiniz.

Time | Value
------------ | -------------
1589189388597 | 32.4
1589189406480 | 27.2
1589189513721 | 15.0

Hadi bu *data frame*'den nasıl veri çekip görselleştireceğinize bakalım:

1. Her sütundan `number` veri yapısındaki son veriyi alın ve `SimplePanel.tsx` dosyasına `return` kısmından önce aşağıdakini kullanarak ekleyin:
```typescript
const radii = data.series
    .map(series => series.fields.find(field => field.type === 'number'))
    .map(field => field?.values.get(field.values.length - 1));
```

`radii` data source'dan gelen serilerden en sondaki verileri içerecek. Bu verileri her çemberin yarıçapını ayarlamak için kullanabilirsiniz.

2. `svg` elementini aşağıdakine göre değiştirin:
```typescript
      <svg
        className={styles.svg}
        width={width}
        height={height}
        xmlns="http://www.w3.org/2000/svg"
        xmlnsXlink="http://www.w3.org/1999/xlink"
        viewBox={`0 -${height / 2} ${width} ${height}`}
      >
        <g fill={color}>
          {radii.map((radius, index) => {
            const step = width / radii.length;
            return <circle r={radius} transform={`translate(${index * step + step / 2}, 0)`} />;
          })}
        </g>
      </svg>
```

Her `radii` değeri için nasıl `<circle>` elementi oluşturduğumuza dikkat edin:

```typescript
{radii.map((radius, index) => {
  const step = width / radii.length;
  return <circle r={radius} transform={`translate(${index * step + step / 2}, 0)`} />;
})}
```

Oluşan çemberi yatay olarak dağıtmak için `transform`'u kullanıyoruz.

3. Plugininizi yeniden build edin ve dashboard'u yenileyin.
```
yarn build
```{{execute}}

Eğer *data frame*'ler hakkında daha çok bilgi sahibi olmak istiyorsanız [Data frames](https://grafana.com/docs/grafana/latest/developers/plugins/data-frames/) sayfasına gidin.
