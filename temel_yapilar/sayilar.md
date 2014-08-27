# Sayılar

Program dediğimiz şey aslında veri + algoritma karışımından oluşmaktadır. Temel yapılar başlığı altında, veri dediğimiz kısmın çok az bir bölümünden bahsedeceğiz. Bu yapıların ilki, matematiğin de temeli olan sayılardır.

Zamanında hayvanları bitkileri saymak için kullandığımız sayıları Erlang altında da aynı o zamanlardaymış gibi kullanabilirsiniz. Hem de o zamanın şartlarına ve imkanlarına çok fazla gelecek şekilde.

Çok fazla konuşmak yerine doğrudan işimize dönelim. Öncelikle önümüzde açık olan Erlang shell altında temel dört işlem yapalım.

```erlang
1> 15 + 457.
472
2> 234512 * 15678.
3676679136
3> 653231 / 2331.
280.23637923637926
4> 765785675 rem 123211
4> .
29310
5> 123543534 div 56.
2206134
```

`1>` ilk yazdığımız komutu göstermektedir. Artan sırada sayılar ile de sonraki komutlar gelmektedir.

İlk yazdığım kod `15` ile `457` sayısını toplamaktadır. Bunu rahatlıkla anladığınızı düşünüyorum. Ancak sonuna neden nokta koyduğumu düşünebilirsiniz. Çok doğal. Bu yüzden bilmemiz gereken ilk kuralı açıklıyorum.

> Erlang yazarken kod parçalarımızın sonuna '.' koyuyoruz!

Tabi her kod parçasının sonuna nokta koyulmaz. Nereye koyup koyulamayacağını zamanla siz zaten rahatlıkla anlayacaksınız.

Erlang shell altında çalışırken eğer nokta koymazsanız ifadenizin değerlendirilmediğini `4>` kısmından görebilirsiniz. Bu blok içerisinde yer alan `rem` ifadesi `remainder` ingilizce kelimesinin kısaltmasıdır ve `kalan` anlamına gelmektedir. Aynı şekilde `5>` bloğu içerisinde yer alan `div` ifadesi `bölüm` anlamına gelmektedir.

Kodlarınız altında büyük sayılar ile rahatlıkla işlem yapabileceğinizi aşağıdaki kod parçası ile gösterebiliriz.

```erlang
6> 432746237846237846273832131231231231246238764283 * 238472384723849723842384723892819731829739218.
103198027319466609390776466851702102060477505109241855226701882962538115889351785590462750694
```

Çeşitli matematiksel ifadeleri de aynı kağıda yazıp çözer gibi Erlang'a yaptırabilirsiniz.

```erlang
7> 1231231 + (23213*312312) + (567-123)/3 + 12*3 + 22/7 + 56*123 + 45.6.
7250936807.742858
```

Bu muhteşem dil ile sabaha kadar bakkal hesabı yapacak değiliz. İşin içine biraz bilgisayar matematiği katalım ve sayıları istediğimiz tabanda değerlendirelim ve işleme sokalım.

```erlang
8> 2#110111.
55
9> 2#110111 + 2#101 + 2#11111.
91
10> 8#0556 + 8#45454.
19610
11> 16#DEADBEEF + 16#DEDE.
3735985613
```

`8>` satırında 2'li tabanda yer alan `110111` sayısını görmek istediğimizi belirtiyoruz. Gelen sonuç gerçekten `32 + 16 + 4 + 2 + 1` ifadesinin sonucuna eşit olduğunu görebiliriz. Bir sonraki satırda da ikili tabanda çeşitli sayılar oluşturup bunlar üzerinde toplama işlemi yapıyoruz. Devamında yer alan kısımlarda da benzer şekilde farklı tabanlar üzerinde işlem yapabileceğimizi görüyoruz. İlla toplama işlemi yapacağımız aklınıza gelmesin. Aşağıdaki örnek çok daha genel bir sonucu içeriyor. Hayran kalın!

```erlang
12> 2#1011 * 8#666 + 16#FFF * 2#1111.
66243
```
