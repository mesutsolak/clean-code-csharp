# clean-code-csharp
Clean Code

Enum oluştururken isimlendirmelerin sonuna çoğul eki gelmez.Örneğin : Roles yerine Role olarak kullanılması gerekmektedir.Enum başlangıcında genellikle None kullanılır.Her oluşturulan enum , enums klasörünün altında tutulması tavsiye edilir.

```C#

public enum Role
{
   None,
   Admin,
   User
}

```
