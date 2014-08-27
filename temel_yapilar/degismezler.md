# Değişmezler

Öncelikle bu ismi ben uydurduğumu söylemek istiyorum. Mantık olarak tam istediğimi ifade ediyor mu bilmiyorum. Sizler zaten birkaç örnek sonra demek istediğimi anlayacağınız için çok da önemli değil.

Diğer diller içerisinde verilerimizi tutmak için değişkenler tanımlarız. Adı üstüne bu değişkenler zamanla **değişir**. Kendiliğinden değişmese bile **değiştirilebilir**. Ancak fonksiyonel dillerin getirdiği yapı gereğiyle değişkenler **değiştirilemez**. Bu yüzden onlara **değişken** demek bence çok doğru değil. Ben şimdilik eski dostumuz **değişkenlere** kısa süreliğine **değişmezler** demek istiyorum.

```erlang
1> ErlangCikisTarihi = 1986.
1986
2> ErlangCikisTarihi = 2014.
** exception error: no match of right hand side value 2014
3> 1986 = ErlangCikisTarihi.
1986
```

Örneğin `ErlangCikisTarihi` isimli eski ismiyle bir **değişken** yeni adıyla bir **değişmez** tanımlayalım ve içerisine `1986` değerini koyalım. Bu işlem `1>` kısmından görülebilir. Burada yaptığımız işlem bellekten yer tahsisi yapıp içerisine ilgili verimizi koymaktadır. Neredeyse tüm dillerin sağladığı bu özelliği biz de Erlang altında yukarıdaki formda gerçekleştiriyoruz. Burada hemen ikinci kuralımızı belirtelim.

> Erlang'da değişmezler büyük harf ile başlar!

Sol tarafa yazdığımız büyük harf ile başlayan tanımlayıcıya eşittirin sağ tarafında yazdığımız değeri atadır. Buradaki atama işlemi aslında Erlang bilenler tarafından doğrudan bellek tahsisi olarak nitelendirilmez. Şimdilik biz bu şekilde yapıldığını düşünerek yolumuza ilerleriz. Kim bilir belki ilerde bu konuyu bile anlatırım!

Peki o kadar **değişmez** dedin de gerçekten **değişmediğini** nereden bilelim. `2>` kısmında tüm söylediklerimi doğruladım. `ErlangCikisTarihi`'ni `2014` yapmaya çalışırken yakalandık! Eğer bunu yapabilseydik Erlang'ı baştan yazdım diyebilirdik. Neyse ki korkulan olmadı. Değeri değiştiremedik.

`3>` satırında da az önce söylediğim aslında bu işlemin diğer dillerdeki gibi bir atama işlemi olmadığını doğrulamış olduk. Burada gerçekleşen olay `pattern matching` olarak isimlendirilir. İlerleyen zamanlarda bolca karşılaşacağız zaten. Şimdilik iyi bir şey olduğunu bilsek yeter.

```erlang
4> _ = 15.
15
5> 15 = _.
* 1: variable '_' is unbound
```

Yukarıdaki kod parçasından da yeni bir şey öğreniyoruz. `_` geçici olarak bir değer tutabilir. Aslında tutarmış gibi gösterebilir demek daha doğru olur. Gerçekten tutmadığını da `5>` satırından görebilirsiniz.
