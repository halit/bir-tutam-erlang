# Atomlar

Maddenin temel yapıtaşı olan atomlardan esinlenilerek oluşturulduğunu düşündüğüm `atom` yapısı sadece Erlang değil diğer birçok fonksiyonel dilde karşınıza çıkabilir. İsminden bile yola çıkarak rahatlıkla mantık yürütebiliriz.

```erlang
1> ahmet.
ahmet
2> mehmet.
mehmet
3> ahmetlerin@mehmet.
ahmetlerin@mehmet
4> 'halit@ziya@usakligil'.
halit@ziya@usakligil
```

Çok fazla konuşmadan doğrudan kod üzerinde gösterme yapalım. `1>` satırında örnek bir atom olan `ahmet` gözükmekte. Burada kafanız biraz karışabilir. Bunun sebebi kesinlikle diğer dillerden kazandığınız alışkanlıklardır. Eliniz sürekli sağ tarafa eşittir yazıp bir değer koymaya gidebilir. Aman diyim uzak durun.

Buradaki `ahmet` yapısının anlamı aslında sayılar kısmında gördüğümüz `5`, `6` gibi değerlerden hiçbir farkı yok. Ama sadece yapılarının anlamı açısından ufak farklar mevcut.

`atom` yapısında değerler oluştururken küçük harf ile başlayabilirsiniz, içerisinde `@`, `_` gibi karakter kullanabilirsiniz ve `' '` tek tırnak içerisine alabilirsiniz.

> Tek tırnak olayına dikkat! Çift tırnak değil!

Bu `atom` yapısını kafanızda daha güzel canlandırmak isterseniz renkleri düşünebilirsiniz. Renkler gayet güzel atomlardır. Eğer kodunuz içerisinde renkler ile işiniz varsa `atom` yapısı bu iş için idealdir.

> Değişmezlerin büyük harf, atomların küçük harf ile başladığına dikkat!

Erlang öyle her küçük harf ile başlayanın atom olmasına izin vermez. Atom olmayacak isimler aşağıda yer almaktadır.

`after`,`and`,`andalso`,`band`,`begin`,`bnot`,
`bor`,`bsl`,`bsr`,`bxor`,`case`,`catch`,`cond`,
`div`,`end`,`fun`,`if`,`let`,`not`,`of`,`or`,
`orelse`,`query`,`receive`,`rem`,`try`,`when`,`xor`
