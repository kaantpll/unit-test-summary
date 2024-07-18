### Unit Test Çalışırken Aldığım Notlar.

### Unit Test Nedir ?
Unit Test, yazdığımız kodların en küçük parçalarını istediğimiz gibi sonuç verip vermediğini
doğruladığımız testlerdir. Bu testler her şeyden bağımsız ve izoledir. 

### Unit Testin Amacı Nedir ? 
Unit Test yazmamızdaki ana amaç kodun sürdürülebilirliğini sağlamaktır. Daha detay verecek olursam
çalıştığımız projelerin çoğu yıllar boyu geliştiriliyor ve büyük bir codebase'imiz oluyor. Bu kod 
büyüdükçe bizim eski kodlara müdahele etmemiz riskli hale geliyor çünkü değiştireceğimiz yerin etki
ettiği birçok iş akışı olabilir. Eğer testimiz yok ise tek tek kodun nerelere etki ettiğini bulup
tekrar tekrar test etmemiz gerekir. Bu yöntem hem çok zaman alır. Kod bir saatli bomba gibi ne zaman
hata vereceği belli olmaz.


Grafikte görüldüğü gibi test yazmak zaman alan bir süreç ve ilk başlarda ilerlemenizi 
yavaşlatacak bir yöntemdir. Ancak proje büyüdükçe eğer unit testiniz yoksa harcanan efor
gitgide artmaktadır. Belki de bir zaman sonra kodun içinden çıkılmaz bir hal alacaktır.

![Resim Açıklaması](assets/unit_test_1)


### Bir Unit Testi Ne İyi Ne Kötü Bir Test Yapar ? 
Unit Test yazmak projenin bakımı için iyidir fakat iyi yazılmış bir unit test bunu sağlar. Kötü
yazılmış testler işleri yine işin içinden çıkılmaz bir hale getirecektir. Peki iyi unit test için 
neler yapılmalı ; 
 - Öncelikle yazılan kodun çalışma mantığını çok iyi anlamak gerekir.
 - En küçük bir değişiklikte bile unit testler tekrar çalıştırılmalıdır.
 - Kodda bir refaktör işlemi yapıldıysa test kodlarında da refaktör yapılmalıdır.

### Test Kalitesini Ölçerken Test Coverage Araçlarını Kullanma
