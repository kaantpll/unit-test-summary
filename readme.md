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
Test Coverage kodumuzun ne kadarının test edildiğini bize gösterir. Yüksek test covarage daha iyi 
gibi genel bir algı vardır ama bu doğru değildir. İyi analiz edilmemiş, güvenli olmayan ve kalitesiz
testlerde code covarege artırır ama bu testin kaliteli olduğunu göstermez. 
Code covarege hesaplanırken testi yazılmış kod satırı ile toplam kod satırının birbirine olan oranı ile hesaplanır. Bu hesap kod yazımına göre değişebilir ama mantık olarak aynı kapıya yol açsada code covarage oranı değişebilir.

```
function isEligible (int number)
{

 if(number > 3)
   return true;

 return false
}


it('is eligible test')
{
  bool result = isEligible(5);
  assert.equal(false,result)
}

```

Üstteki koddun code covarege oranı hesaplanırken  test edilmiş kod satırı / toplam kod satırı. Bu işlem sonucu 4/5 = %80 code covarage diyebiliriz. (Hesaplanırken süslü parantezlerde dikkate alınmıştır.)  Şimdi kodumuzda bir düzeltme yaptıktan sonraki haline bakalım.

```
function isEligible (int number)
{
   return  number > 2;
}


it('is eligible test'){
  bool result = isEligible(5);
  assert.equal(false,result)
}

```
Kodun refaktör edilmiş hali ile kod %100 code covarage ulaştı ama aslında kodun çalışma mantığında hiçbir değişim olmadı.

Bu örnek ile code covarage oranının yüksek olması ile test kalitesinin ve güvenilirliğinin kesinlikle doğru olmadığını bize göstermiştir.

### Branch Covarage Metric Nedir ? 
Bir başka test covarage oranı hesaplama yöntemi denilebilir. Bu yöntem herkesin bildiğin code covarage hesaplama yönteminden daha doğru sonuçlar verir. Kod satırı toplamları ile değil kontrol yapısına odaklanarak hesap yapılır. Örneğin if veya switch'ler gibi. Branch covarage test = Gezilen branchler / toplam branchler. Örneğin

```
function isEligible (int number)
{
   return  number > 2;
}


it('is eligible test'){
  bool result = isEligible(5);
  assert.equal(false,result)
}

```

Örnek kodda iki tane durum (control) var diyebiliriz. İlki number'ın ikiden büyük olma durumu, ikincisi number'ın ikiden küçük veya eşit olma durumu. Yazmış olduğumuz test ise şuan sadece
bir tane durumu karşılıyor bu da branch code metric ile hesapladığımızda 1/2 = %50 code covarege sağlanmış olduğunu bize gösteriyor.


## Code Metric'lerindeki Problemler
- Kod metrikleri sistemin tamamen test altında olduğunu garanti etmez.
- Kod metrikleri kullandığınız kütüphaneleri teste dahil  etmez.

## Başarılı Test Nasıl Yazılır ?
Aslında bu çok zor bir uğraş. Her olası durumu ele alıp tek tek tüm durumlar için test yazılmalıdır. Tabiki bu zaman ve maliyet olarak dezavantajlı olsada doğrusu budur.

## Unit Testin Anatomisi
### AAA Paterni
AAA paterni unit test yazarken bir standart haline gelmiş bir patterndir. Arrange, Act ve Assert anlamına gelir. Arrange aşaması testi gerçekletirmek için olan verilerin ayarlanması,
act aşaması fonksiyonun çağrıldığı ve son alan olan assert ise fonksiyondan aldığımız
sonucu doğrulama aşamasıdır. Örnek:

```
function sumOfTwoNumbers (int number)
{
   //Arange
   const number1 = 5;
   const number2 = 10;

   // Act
   const result = sum(number1,number2)

  // Assert
  expect(result).toBe(15);
   
}

```

Bu yaklaşım unit test yazmaya bir standart getirir ve kodun okunmasını kolaylaştırır.

### Given-When-Then Paterni
Bu paternde aslında aynı amaçla ortaya çıkmıştır unit test yazmayı bir standart haline
getirmek.
AAA Paternine karşılık gelen alanlar:
 - Given = Arrange,
 - When = Act
 - Then = Assert

```
function sumOfTwoNumbers (int number)
{
   //Given
   const number1 = 5;
   const number2 = 10;

   // When
   const result = sum(number1,number2)

  // Then
  expect(result).toBe(15);
   
}

```

## Birden Çok Arrange, Act ve Assert bölümlerini önlemek.
Öncelikle bir unit test kodunda bu alanlardan hehrhangi birinin birden çok bulunması
kodda bir sıkıntı olduğunu gösteririr ve refactor edilmesi gerektiğini bizlere gösterir.

## Unit Testlerde if durumundan kaçınmak.
Aynı şekilde unit testin içinde if durumu bulunması bir anti-pattern'dir ve kaçınılması gerekir. Unit testlerimizi basit tutmalıyız.

## Kodları Yeniden Kullanma
Unit test yazarken girdi verilerine ihtiyacımız oluyor(arrange kısmı). Bu değerleri bir kere oluşturup daha sonra diğer testler içinde kullanabiliriz.

## Unit Test Isimlendirme
Unit Test fonksiyonunu isimlendirirken kodun nasıl davrandığını açıkca anlatmak gerekir. Birden çok isimlendirme standartı bulunmaktadır. Bunlardan birisi: 
[MethodUnderTest]_[Scenario]_[ExpectedResult]
- MethodUnderTest kısmı test edilen metodun ismi
- Scenario metodun yaptığı iş
- ExpectedResult kısmı ise işlem sonucu beklenen çıktı

Bu isimlendirme standardı bazı zamanlarda işe yaramayabiliyor çünkü bazen detaylar yerine davranışı test etmemiz gerekiyor. 
sayfa 55 başında.





