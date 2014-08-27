# Kurulum

Ağzınızda bir tutam Erlang tadı bırakabilmek için tabiki de çeşitli araçlara ihtiyaç duyacağız. Bunların başında yazdığımız kodları çalıştıracak bir yorumlayıcı geliyor. Bu kurulumdan hemen sonra en çok sevdiğiniz editöre de Erlang eklentisini kurursanız tadından yenmez. Piyasada çok fazla editör bulunduğundan herbiri için kurulum aşamasını anlatmayacağım. Siz kendi editörünüz için doğru ortamı kurmakta özgürsünüz. Ama vim kullanıcılarına [buradaki][3] blog yazısını okumalarını tavsiye ederim.

## Linux

### Debian Tabanlı(Ubuntu, Mint vb)

```sh
apt-get install erlang
```

### Arch

```sh
pacman -S erlang
```

### Rpm tabanlı(Centos, Fedora vb)

```sh
yum install erlang
```

## FreeBSD

```sh
portmaster lang/erlang
```

veya

```sh
cd /usr/ports/lang/erlang; make install clean
```

veya

```sh
pkg_add -rv erlang
```

## OSX

```sh
brew install erlang
```

veya

```sh
port install erlang
```


## Diğer işletim sistemleri

Erlang'ın diğer işletim sistemleri için gerekli olan kurulum dosyalarına [buradaki][1] linkten ulaşabilirsiniz.


## Kurulum sorunları

Kurulum sırasında bir sorun ile karşılaşırsanız öncelikle Erlang'ın kendi [web][2] sayfasından indirme yaparak tekrardan denemelisiniz. Eğer daha başka bir sorun ile karşılaşırsanız bu sefer google en büyük yardımcınız olacaktır. Emin olun sizden önce onbinlerce insan da aynı duruma düştü!

[1]: https://www.erlang-solutions.com/downloads
[2]: http://www.erlang.org/download.html
[3]: http://blog.erlware.org/2013/09/09/how-to-use-vim-for-erlang-development/
