# Listeler

Farklı tipteki verileri bir arada tutmanın birçok dildeki en kolay yolu listeleri kullanmaktır. Kolay olduğu gibi bir o kadar da esnektirler. Sırf onlar üzerinde rahat işlem yapabilmek için `Lisp` gibi devasa bir dil bile bulunur. Bu dil gücünü listelerden aldığına göre, listelerin gücünü başka şekilde anlatmaya gerek yoktur.

Bu veri tipinin en önemli özelliği farklı tipteki verileri de bir arada tutabiliyor olmasıdır. Farklı veri tiplerinin yanında kendi tipinde yani başka bir listeyi de içinde tutabilir.

Erlang dilinde yeni bir liste  `[Eleman1, Eleman2, ... , ElemanN]` şeklinde oluşturulur.

```erlang
1> [23, 15, {okuz, sigir, at, manda, [1,2,3]}, 3.14159265538979323846]
1> .
[23,15,{okuz,sigir,at,manda,[1,2,3]},3.1415926553897933]

```

Burada listenin sonuna nokta koymadığım zaman işleme alınmadığını farketmiş olmalısınız. Bu en başlardan beri söylediğim bir kuraldan dolayıdır. İfadelerinizin bittiğini Erlang'a söylemelisiniz.

`1>` satırında gördüğünüz liste `4` adet eleman içermektedir. Bunlardan ilk ikisi `23` ve `15` sayısıdır. Daha sonraki eleman bir `tuple` veri tipidir ve içerisinde en başta `4` tane hayvan isminden oluşmuş `atom` vardır. Bu hayvan isimlerinden hemen sonra içerisinde 1'den 3'e kadar olan sayıları içeren bir adet daha liste gelmektedir. Bu `tuple` veri tipinden hemen sonra da bir adet kayan noktalı sayı gelmektedir.

```erlang
2> [111, 104, 97, 32, 108, 97, 110].
"oha lan"
```

Evet fark ettiğiniz üzere sayıların `ascii` karşılıklarına göre değerlendirerek bizim sayı listemizi `string` haline getirdi. İlk defa görünce şaşırabilirsiniz ama çok fazla kafanıza takmayın bunu.

> Ekrana basılabilir `ascii` değerleri içeren sayı listeleri string olarak değerlendirilir!

```erlang
3> [111, 104, 97, 32, 108, 97, 110, 1].
[111, 104, 97, 32, 108, 97, 110, 1]
```

`3>` nolu satırdan gördüğünüz gibi `liste` içerisinde ekrana basılabilir bir `ascii` değeri olmadığında normal olarak değerlendiriliyor.

Yazdığımız kodlar içerisinde bolca `liste` kullanacağımız için üzerinde yapacağımız işlemleri çok iyi bilmemiz gerekiyor.

```erlang
4> [2,3,5,7,11,13,17,19,23] ++ [29,31,37,41].
[2,3,5,7,11,13,17,19,23,29,31,37,41]
5> [2,3,5,7,11,13,17,19,23] -- [7,11,2,23].
[3,5,13,17,19]
6> [5,7,11,13] -- [5,7,11,13].
[]
7> [3,4] ++ [1,2] ++ [4] ++ [1,1,1,1,1].
[3,4,1,2,4,1,1,1,1,1]
```

İki listeyi birbirine bağlamak için `++` kullanılabilir. Buradan bağlamaktan kastım uçuca eklemektedir. Bu operatör sağ taraftan birleşme kuralına sahip olduğu için işlemler `sağdan sola` doğru gerçekleşir.

`4>` satırında iki adet listeyi birbirine ucuca eklediğimiz görülebilir. `5>` satırında yaptığımız işlemin çok daha etkileyici gözükmesi lazım.

```python
In [1]: [2,3,5,7,11,13,17,19,23] + [29,31,37,41]
Out[1]: [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41]

In [2]: [2,3,5,7,11,13,17,19,23] - [7,11,2,23]
...
TypeError: unsupported operand type(s) for -: 'list' and 'list'
```

Yukarıda gözüken kod kısmı `Python` dilinde az önce gösterdiğimi `liste` işlemlerinin benzerlerinin sonuçlarıdır. İki listeyi toplamak için `+` operatörü gene kullanılabilir durumdadır. Ancak bir liste içerisinden bir liste çıkarmayı denediğinizde hata almalısınız. (Bunun anlamı `Python` dili zayıf demek değildir. Her dilin kendine göre üstün ve zayıf yanları vardır. Sadece yeri geldiği için gösterdiğim bir örnektir. Yukarıdaki çıkarma işlemini `Python` dilinde de `set` veri tipi ile gerçekleştirebilirsiniz)

Kısa bir `Python` turundan hemen sonra `6>` satırından devam edelim. Burada bir listenin içerisinden kendisiyle aynı içeriğe sahip başka bir listeyi çıkardığımızda boş liste elde ettiğimizi görebiliriz. Hemen ardından `7>` satırında birden çok listenin nasıl eklendiği görülebilir. Aynı şekilde birden fazla çıkarma işlemi de yapılabilir. Ancak bunu yaparken sağdan birleşme kuralının olduğu unutulmamalıdır.

> `++` ve `--` sağdan sola doğru çalışmaktadır!

```erlang
8> BenimPazarListem = [elma, armut, karpuz, kiraz, visne].
[elma,armut,karpuz,kiraz,visne]
9> [IlkAlinacak|DigerAlinacaklar] = BenimPazarListem.
[elma,armut,karpuz,kiraz,visne]
10> IlkAlinacak.
elma
11> DigerAlinacaklar.
[armut,karpuz,kiraz,visne]
12> hd(DigerAlinacaklar).
armut
13> tl(DigerAlinacaklar).
[karpuz,kiraz,visne]
14> hd(tl(tl(DigerAlinacaklar))).
kiraz
```
Şimdi biraz daha `liste` işlemleri görelim. `8>` satırında `BenimPazarListem` diye içerisinde pazardan alınacak `atom` veri tipindeki meyveleri tutan liste oluşturdum. `9>` satırında da değişmezler konusu sırasında ilk defa bahsedilen `pattern matching` işlemi ile listenin ilk elemanını `IlkAlinacak` değişkenine, geri kalanı da `DigerAlinacaklar` değişkenine atadık. Eğer bu `pattern matching` kavramı hala kafada soru işareti bırakıyorsa hemen şimdi araştırma yapıp iyice öğrenilmeli.

`10>` ve `11>` satırlarında listenin ilk kısmı ile geri kalanını gerçekten aldığımızı görebiliriz. Burada yaptığımız işlem için ön tanımlı `hd` ve `tl` diye iki adet fonksiyon vardır. `hd(head)` ile listenin ilk elemanına ulaşabiliriz. `tl(tail)` ile de listenin ilk elemanı hariç geri kalan listeye ulaşabiliriz. `14>` satırında da bu fonksiyonların arka arka birkaç kombinasyonu görülmektedir.

```erlang

15> [Ilk, Ikinci|Diger] = BenimPazarListem.
[elma,armut,karpuz,kiraz,visne]
16> Ilk.
elma
17> Ikinci.
armut
18> Diger.
[karpuz,kiraz,visne]
```

`pattern matching` konusunda bir örnek daha yapalım. `15>` satırında az önce oluşturduğumuz `BenimPazarListem` listesi içerisindeki ilk elemanı `Ilk` isimli değişkene, ikinci elemanı `Ikinci` isimli değişkene ve geri kalan elemanları da `Diger` isimli değişkene atadık.

> Değişken dediğime bakmayın, değişmez onlar!

Listeler ile ilgili son söylenmesi gereken `|` sembolünün birleştirici bir eleman olduğudur. Yeni bir liste oluşturmak istediğinizde verilerin arasında bu arkadaşı almanız yeterlidir.

```erlang
19> [15 | [16 | [17 | []] ] ].
[15,16,17]
```

`19>` satırında görüldüğü gibi `|` ifadesi sayesinde boş listeler ile değerleri birleştirebiliyoruz. Ancak `|` liste birleştirmek için değil yeni bir liste oluşturmak için kullanılır. Diğer fonksiyonel dillerdeki ismi `cons`dur.
