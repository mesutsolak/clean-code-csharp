# clean-code-csharp
Clean Code

## İç içe foreach

İç içe foreach kullanmakta kodun okunmasını ve kalitesini düşürmektedir.Bunların yerine tercih edebileceğimiz bazı kod yazım şekilleri aşağıda belirtiğim gibidir.

```C#
foreach(Customer c in Customers)
{
  foreach(Order o in c.Orders)
  {
    o.Calculate();
  }
}

//instead

foreach(Order o in Customers.SelectMany(c => c.Orders))
{
  o.Calculate();
}

Or

void SubmitOrders()
{
    var orders = GetOrders()
    foreach (Order o in orders)
    {
        SubmitOrder(o);
    }
}

void SubmitOrder(Order order)
{
    foreach (OrderDetail d in order.Details)
    {
        // ...
    }
}
```

## Debug Mod Belirtme 

Kodlarımızın sadece debug modda çalışmasını istediğimizde if debug koymak yerine Conditional attribute'unu kullanmamız okunabilirliğini arttıracaktır.

```C#
#if DEBUG
  int amount = 5;
  int newAmount = amount += 1;
#endif

[Conditional("Debug")]
private void AmountValue()
{
    int amount = 5;
    int newAmount = amount += 1;
}
```

## Null Kontrolü

Uygulama içerisinde null check kontrolü kullanırken != null yazmaktansa ? işareti koyarak aynı işlevi sağlayabiliriz.

```C#
double? amount = null;
PhoneNumber p = null;

if ((amount ?? 0) > 0)
{

}

if (string.IsNullOrWhiteSpace(p?.Number))
{

}
```
Bir kod blogu içerisinde çok fazla ? ve ?? işareti kullanmakta kodun okunabilirliğini zayıflatacaktır.Bu tip bir durumda != null kullanmak daha doğru olacaktır.

```C#
var name = person?.Name ?? string.Empty;
var phoneNumbersCount = person?.PhoneNumbers?.Count() ?? 0;
var surname = person?.Surname ?? string.Empty;

//instead
if (person != null)
{

}
```



## Enum

Enum oluştururken isimlendirmelerin sonuna çoğul eki gelmez.Örneğin : Roles yerine Role olarak kullanılması gerekmektedir.Enum başlangıcında genellikle None kullanılır.Her oluşturulan enum , enums klasörünün altında tutulması tavsiye edilir.

```C#

public enum Role
{
   None,
   Admin,
   User
}

```

## Sabit Tanımlama

Uygulama içerisinde değişmeyecek değerlerin const olarak tanımlanması gerekmektedir.

```C#
public const string TEXT_FORMAT = "{0} {1}";
```
