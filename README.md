# S7-1200 ile Analog Basınç Ölçümü ve Ölçeklendirme

Bu kişisel çalışmada, Factory I/O ortamında oluşturulan 0–10 V analog sinyal, TIA Portal üzerinden işlenerek 0–500 mbar aralığında bir basınç değerine ölçeklendirilmiştir.

Uygulama, Siemens S7-1200 PLC programı ve S7-PLCSIM kullanılarak simülasyon ortamında gerçekleştirilmiştir.

## Çalışmanın Amacı

- Analog giriş verisinin PLC tarafından okunması.
- INT veri türünün REAL veri türüne dönüştürülmesi.
- Matematiksel işlemlerle analog giriş değerinin basınç birimine ölçeklendirilmesi.
- Farklı giriş değerlerinde hesaplanan sonuçların izlenmesi.

## Kullanılan Yazılımlar

- TIA Portal V18
- Siemens S7-PLCSIM
- Factory I/O

## Programın Çalışma Mantığı

1. Factory I/O üzerindeki analog sinyal, **%IW30** giriş adresinden okunur.
2. **MOVE** komutu ile giriş değeri **%MW10** adresine aktarılır.
3. **CONV** komutu ile **INT → REAL** dönüşümü gerçekleştirilir ve sonuç **%MD12** adresine yazılır.
4. **MUL** komutu ile değer **500.0** ile çarpılır ve sonuç **%MD16** adresine yazılır.
5. **DIV** komutu ile sonuç **27648.0** değerine bölünür.
6. Hesaplanan basınç değeri **%MD20** adresinde tutulur.

### Ölçeklendirme Formülü

**Basınç (mbar) = Analog giriş değeri × 500.0 / 27648.0**

### Kullanılan Adresler

| Adres | Açıklama |
|---|---|
| %IW30 | Analog girişin ham değeri |
| %MW10 | MOVE komutuyla aktarılan tam sayı değeri |
| %MD12 | REAL türüne dönüştürülen değer |
| %MD16 | 500 ile çarpılan ara sonuç |
| %MD20 | Hesaplanan basınç değeri |

## Simülasyon Sonuçları

| Analog Giriş | Ham Değer | Hesaplanan Basınç |
|---|---:|---:|
| 0 V | 0 | 0 mbar |
| Yaklaşık 5 V | 13935 | Yaklaşık 252,0074 mbar |
| 10 V | 27648 | 500 mbar |

**Not:** Orta noktadaki ekran görüntüsünde giriş göstergesi 5,0 V olarak görünürken ham değer 13935'tir. Bu nedenle hesaplanan sonuç yaklaşık 252 mbar'dır. Tam orta noktaya karşılık gelen 13824 ham değeri ise 250 mbar verir.

## Uygulama Görselleri

### 1. Factory I/O Bağlantısı ve Adres Eşleştirmesi

Factory I/O üzerinde **Siemens S7-PLCSIM** sürücüsü seçilmiş ve analog sinyal **%IW30 (INT)** giriş adresiyle eşleştirilmiştir.

![Factory I/O bağlantısı ve adres eşleştirmesi](<Factory IO bağlantı ve adres eşleştirmesi.png>)

### 2. 0 V Giriş — 0 mbar Sonucu

Analog giriş değeri **0** olduğunda, ölçeklendirme sonucunda hesaplanan basınç **0 mbar** olur.

![0 V giriş ve 0 mbar sonucu](<0 V giriş, 0 mbar sonucu.png>)

### 3. Yaklaşık 5 V Giriş — Yaklaşık 252 mbar Sonucu

Analog girişten okunan **13935** ham değeri, programdaki dönüşüm ve matematiksel işlemler sonucunda yaklaşık **252,0074 mbar** olarak hesaplanmıştır.

![Yaklaşık 5 V giriş ve 252 mbar sonucu](<Yaklaşık 5 V giriş, 252 mbar sonucu.png>)

### 4. 10 V Giriş — 500 mbar Sonucu

Analog girişten okunan **27648** ham değeri, ölçeklendirme sonucunda **500 mbar** olarak hesaplanmıştır.

![10 V giriş ve 500 mbar sonucu](<10 V giriş, 500 mbar sonucu.png>)

## Proje Dosyası

[TIA Portal proje arşivini indir](<S7-1200 ile Analog Basınç Ölçümü ve Ölçeklendirme.zap18>)

## Çalışmanın Kapsamı

Bu çalışma bir simülasyon uygulamasıdır. Basınç değeri, Factory I/O ortamında oluşturulan analog sinyalin 0–500 mbar aralığına ölçeklendirilmesiyle elde edilmiştir.

**Hazırlayan: Mustafa Şahin**
