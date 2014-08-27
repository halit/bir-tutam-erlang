# Demetler

Bu yapıya demet dediğim için belki tanıyamayanlar olabilir ama bildiğimiz `tuples` tipinden bahsedeceğim. Erlang içerisinde demetler `{Eleman1, Eleman2, ... , ElemanN}` formunda tanımlanırlar.

```erlang
1> Yukseklik = 190, Genislik = 30.
30
2> Ebat = {Yukseklik, Genislik}.
{190,30}
3> Ebat = {190, 30}.
{190,30}
4> Ebat = {190, 40}.
** exception error: no match of right hand side value {190,40}
```
`1>` satırında öncelikle `Yukseklik` ve `Genislik` isimli değişmezlerimize 190 ve 30 değerlerini atadık. Daha sonra `2>` satırında `Ebat` isminde bir demet oluşturduk. En başta bahsettiğim forma gayet uygun. Gerçekten eşit olup olmadığını da `3>` satırındaki kontrolun sonucundan anlayabiliriz. Farklı bir değer ile kontrol etmeye çalışırsak alacağımız hata da `4>` satırında yer alıyor.

```erlang
5> {X, _} = Ebat.
{190,30}
6> X.
190

```

`5>` satırında değişmezler kısmında bahsettiğim boş işler bakanı `_` ile çok güzel bir `pattern matching` yapıyoruz. `X` isimli değişkene `Ebat` demetinin ilk elemanını atıyoruz ve ikinci eleman ile ilgilenmediğimizi `_` kullanarak belirtiyoruz. Gerçekten bu elemanın `X` içerisine girip girmediğini `6>` satırındaki kontrolümüz ile anlayabiliriz.

Demet veri yapısı diğer türlerden biraz daha farklıdır. Çünkü bu yapı ile yeni yapılar türetebiliriz. Aynı C dilinde yer alan `struct` misali demetleri kullanabiliriz.

```erlang
7> Mehmet = {{isim, "mehmet"}, {yas, 20}, {boy, 160}, {kilo, 55}}.
{{isim,"mehmet"},{yas,20},{boy,160},{kilo,55}}
8> {{_, _}, {_, MehmetinYasi}, {_, MehmetinBoyu}, {_, MehmetinKilosu}} = Mehmet.
{{isim,"mehmet"},{yas,20},{boy,160},{kilo,55}}
9> MehmetinYasi.
20
10> MehmetinBoyu.
160
11> MehmetinKilosu.
55
```

Yukarıdaki kod parçasında öncelikle `Mehmet` isminde bir adet iç içe demet yapısı oluşturduk. Burada yer alan `yas` yapısının bir `atom` olduğu ve yanında da `20` sayısını taşıdığını görebilirsiniz. Bu şekilde birçok veriyi tek bir yapı altında toplamış olduk. `8>` satırında da bu yapı içerisinden bazı yapıları değişmezlere çıkardık. `MehmetinYasi`, `MehmetinBoyu`, `MehmetinKilosu` yapılarının birer değişmez olduğunu baş harfinin büyük olmasından anlamış olmalısınız.
