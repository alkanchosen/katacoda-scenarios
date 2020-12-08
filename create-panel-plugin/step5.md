## 5. Panel seçenekleri ekleyin

Bazen plugininizin davranışı düzenlemek için kullanıcılara seçenek vermek isteyebilirsiniz. Plugininizde panel seçenekleri ekleyerek panelinizin kullanıcı komutlarını kabul etmesini sağlayabilirsiniz.

Önceki adımda kodunuzda çemberin `fill` rengini değiştirmiştiniz. Şimdi kodu kullanıcıların panel editörü kullanarak bu `fill` rengini değiştirmelerine izin verecek şekilde düzenleyelim.

** Kodları yazarken boşlukları (indendation) unutmayın, yoksa plugin'i build ederken *Linting* aşamasında hata alırsınız.**

### Bir seçenek ekleyin

Panel seçenekleri bir *panel options objesinde* bulunmaktadır. `SimpleOptions` bu objeyi açıklayan bir arayüzdür.

1. `types.ts` dosyasında kullanıcıların aralarından seçebileceği bir `CircleColor` type'ı ekleyin.

```typescript
type CircleColor = 'red' | 'green' | 'blue';
```
2. `SimpleOptions` arayüzünde `color` adında yeni bir seçenek ekleyin.

```typescript
color: CircleColor;
```

Güncellenmiş `types.ts` şu şekildedir:

**src/types.ts**

```typescript
type SeriesSize = 'sm' | 'md' | 'lg';
type CircleColor = 'red' | 'green' | 'blue';

// interface defining panel options type
export interface SimpleOptions {
  text: string;
  showSeriesCount: boolean;
  seriesCountSize: SeriesSize;
  color: CircleColor;
}
```

### Seçenek kontrolü ekleyin

Seçeneği panel editöründen düzenlemek için `color` seçeneğini bir seçenek kontrolüne bağlamanız gerekmektedir.

Grafana çeşitli seçenek kontrollerini destekler: Yazı girişleri, switchler, radio butonlar...

Hadi bir radio kontrolü yaratalım ve `color` seçeneğine bağlayalım.

1. Kontrolü `src/module.ts` dosyasında builder'in sonuna ekleyin.

```typescript
    .addRadio({
      path: 'color',
      name: 'Circle color',
      defaultValue: 'red',
      settings: {
        options: [
          {
            value: 'red',
            label: 'Red',
          },
          {
            value: 'green',
            label: 'Green',
          },
          {
            value: 'blue',
            label: 'Blue',
          },
        ],
      },
    });
```

`path`, kontrolü bir seçeneğe bağlamak içindir. Kontrolü iç içe bir seçeneğe tam konumunu göstererek bağlayabilirsiniz. Örnek: `colors.background` .

Grafana sizin için bir seçenek editörü yaratır ve bunu **Display** bölümündeki *panel editor* kısmında gösterir.

### Yeni seçeneği kullanın

Neredeyse bitti. Yeni bir seçenek ve bu seçeneğin değerini değiştirmek için gerekli kontrolü eklediniz. Fakat plugin bu seçeneği hala kullanmıyor. Hadi bunu düzeltelim.

1. Seçenek değerini mevcut tema tarafından kullanılan renkler yerine koymak için `SimplePanel.tsx` dosyasına `return` kısmından önce yeni bir `switch` kısmı ekleyin.

**src/SimplePanel.tsx**

```typescript
  let color: string;
  switch (options.color) {
    case 'red':
      color = theme.palette.redBase;
      break;
    case 'green':
      color = theme.palette.greenBase;
      break;
    case 'blue':
      color = theme.palette.blue95;
      break;
  }
```

2. Çemberi yeni rengi kullanması için değiştirin.

```typescript
<g>
  <circle style={{ fill: color }} r={100} />
</g>
```

Artık panel editörde Display kısmından Circle color seçeneğindeki rengi değiştirdiğinizde çemberin rengininde değiştiğini göreceksiniz. 
