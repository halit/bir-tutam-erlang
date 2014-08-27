# Bit düzeyi yapılar

Listeler, demetler veya herhangi bir gelişmiş veri yapısı üzerinde işlem yapmak ne kadar önemli ise bit düzeyi yapılarda işlem yapmak da en az o kadar önemlidir. Dilin programcıya bu tarz imkanlar sağlaması gayet önemlidir. Erlang bu açıdan programcısına gayet esnek ve gelişmiş şartlar sunmaktadır. Bu başlık altında bu yapılara temel bir bakış atacağız.

Bit düzeyi yapılara geçmeden hemen önce 16'lı tabandaki sayılar ve okunuşlarından kısaca bahsetmek istiyorum. Örneğin `1f3778` şeklinde bir sayı olsun. Bu sayıyı okumak için ikili bloklara ayırabiliriz. 16'lı tabanındaki bir sayı 2'li bloklara ayrılırsa bu ayrılan bloklar 1 `byte` ile temsil edilir. Sayımız üzerinde düşünürsek `1f 37 78` şekline gelir. Aynı şekilde 2'li bloklar yerine birer birer de düşünebiliriz. Bu zamanda her değer 4 bit ile temsil edilir. 4 bit ile temsil edilebilecek sayı miktarı `2^4=16` olduğunu da dikkate alırsak ve 16'lı tabandaki rakamların `0 1 2 3 4 5 6 7 8 9 A B C D E F` olduğunu düşünürsek bazı şeyler kafamızda canlanmış olmalı. Sayımızı `1 f 3 7 7 8` moduna getirdiğimizi düşünelim. Buradaki `1` rakamını 4 bit ile `0001` şeklinde ifade ederiz. Aynı şekilde `f` rakamını da `1111` şeklinde ifade ederiz.

Artık 16'lı tabandaki sayıları okuyabildiğimize göre Erlang'a da okutalım büyük adam olsun. Dil içerisinde bit düzeyi yapıları `<<` ve `>>` ifadeleri arasına alarak belirtiyoruz.

```erlang
1> Mavimsi = 16#1f3778.
2045816
2> <<Mavimsi:24>>.
<<31,55,120>>
3> <<R:8,G:8,B:8>> = <<Mavimsi:24>>.
<<31,55,120>>
4> R.
31
5> G.
55
6> B.
120
```

Örneğe geçmeden hemen önce ufak bir hatırlatma yapmam gerekiyor. Bilgisayar grafiklerinde genellik renkleri belirtmek için 16'lı tabanda 24 bitlik bir sayı kullanırız. Bu 24 bitin 8 bitlik kısımları kırmızı, mavi ve yeşil tonunu belirtmek için kullanılır. Bu ufak bilgiden hemen sonra `1>` satırında `Mavimsi` ismini verdiğimiz bir değişkene 16'lı tabanda olduğunu belirtip `1f3778` değerini atıyoruz. `2>` satırında bit düzeyi yapılar için kullandığımız yapının ufak bir denemesini yapıyoruz. `3>` satırında da az önce denemesini yaptığımız yapının kırmızı, mavi, yeşil tonlarını R, G ve B değişkenlerine alıyoruz. Bunu yaparken hangi değişkenin kaç bit olduğunu da yanına belirtiyoruz. Gördüğünüz gibi 24 bitlik bir değeri 8 bitlik 3 kısma bölmek bu kadar basit.

```erlang
7> <<Kirmizi:8, YesilveMavi/binary>> = <<Mavimsi:24>>.
<<31,55,120>>
8> Kirmizi.
31
9> YesilveMavi.
<<"7x">>
10> <<Bir:8, Iki:8>> = <<YesilveMavi/binary>>.
<<"7x">>
11> Bir.
55
12> Iki.
120
```

Bit düzeyi işlemlerde şimdi biraz daha deneme yapalım. Eelimizde 24 bitlik olduğunu bildiğiniz `Mavimsi` diye bir yapı var. Bu yapının sadece ilk 8 bitini `Kirmizi` değişkenine, geri kalan bitlerini `YesilveMavi` değişkenine atamak için `7>` satırındaki ifade yeterlidir. Gerçekten değerlerin atandığını hemen ardından gelen 2 satıra daha bakarak teyit edebilirsiniz.

Yapıları tanımlarken kullanabileceğimiz tanımlar mevcuttur. Bu yapılar içerisindeki kısımlara doğrudan değer yazabilirsiniz. Değerin yanında `:` ile ayrılmış şekilde boyutunu da yazabilirsiniz. Ayrıca `/` ile ayrılmış şekilde tipini de belirtebilirsiniz.

Burada kullanabileceğimiz tipler `integer`, `float`, `binary`, `bytes`, `bitstring`, `bits`, `utf8`, `utf16`, `utf32` seçeneklerinden birisi olabilir. Burada yazabileceğimiz daha başka tip çeşitleri de mevcuttur. Ancak onlar ihtiyaçlarınıza göre araştırıp bulunacak derinliktedir.

Bit düzeyinde yapılar üzerinde bit düzeyi işlemleri de yapabiliriz. Bu işlemlerden bazıları `bsl`, `bsr`, `band`, `bor`, `bnot` ve `bxor` olarak verilebilir. Bunlardan `bsl` `binary shift left` kıslatmasıdır. Aynı şekilde `band` `binary and` kısaltmasıdır.

```erlang
13> 2#1010 = 2#101 bsl 1.
10
```

Mesela `13>` satırında `101` sayısını 1 adet sola kaydırıyoruz. Haliyle yeni oluşan değerin `1010` olması gerekli. Eğer `no match of right hand side value` tarzı bir hata almadıysak ve sadece değer gördüysek gerçekten birbirine eşit diyebiliriz.

Son olarak neredeyse artık Erlang ile bütünleşmiş bir kod parçasından bahsetmek istiyorum.

```erlang
<<SourcePort:16, DestinationPort:16,
AckNumber:32,
DataOffset:4, _Reserved:4, Flags:8, WindowSize:16,
CheckSum: 16, UrgentPointer:16,
Payload/binary>> = SomeBinary.
```

Yukarıdaki kod parçası binary olarak gelen bir IP pakedini bloklar halinde parçalamaktadır. Bit düzeyindeki yapıların kullanım alanlarına çok güzel bir örnek teşkil etmektedir. Kod içerisindeki `SomeBinary` değişkeninde ethernet kartından aldığınız bir IP pakedinizin olduğunu düşünün. Bunu kuralına uygun bir şekilde ayrıştırmak için wikipedia'dan bulduğunuz IP paket yapısını sol tarafa belirtiyorsunuz. Örneğin ilk 16 bitin kaynak portu gösterdiği, 128 bitten sonra gelen kısmın da yanında taşıdığı veriyi gösterdiğini sadece kuralına uygun olarak yazılmış. Bu mantığı tüm ikili tabandaki formatlara rahatlıkla uygulayabilirsiniz. Mesela resimleri, sıkıştırılmış dosyaları doğrudan tek satır ile parse edebilirsiniz.
