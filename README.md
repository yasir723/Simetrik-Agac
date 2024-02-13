# Simetrik Ağaç
Bu algoritma, verilen iki ağacın simetrik olup olmadığını kontrol eder. `İki ağacın simetrik olması için bir ağacın sol alt ağacı diğer ağacın sağ alt ağacına, bir ağacın sağ alt ağacı ise diğer ağacın sol alt ağacına eşit olmalıdır.` Algoritma, öncelikle iki ağacın her bir düğümünün değerini ve alt ağaçlarını karşılaştırır. Eğer her iki ağacın her bir düğümü ve alt ağaçları simetrikse, ağaçlar simetrik olarak kabul edilir.

# Bu Örnekteki Kullanımı
Bu örnekte, verilen iki ağacın simetrik olup olmadığı kontrol edilecek. Bu nedenle, her iki parametre olan `node1` ve `node2` aynı ağacı göstermelidir. Böylece verilen iki ağaç aynı ağaç yapısı olacak. Bu sayede, karşılaştırma bir ağaç ile kendisi arasında gerçekleştirilmiş olur

<div align="center">
    <h2>Simetrik Ağaç Örnekleri</h2>
    <div align="center">
        <img src="https://github.com/yasir723/Agac-Elemanlari-Yazdirmak-Pre-Order/assets/111686779/6df3b6e5-8f18-4d9a-8b24-1c6a8f628740" width="334">
        <img src="https://github.com/yasir723/Agac-Elemanlari-Yazdirmak-Pre-Order/assets/111686779/5e2c82a7-0746-4b52-a230-fe7246bb0961" width="334">
        <img src="https://github.com/yasir723/Agac-Elemanlari-Yazdirmak-Pre-Order/assets/111686779/2ebf32b5-d000-476d-99e2-870f341162c0" width="334">
    </div>
</div>


<div align="center">
    <h2>Simetrik Olmayan Ağaç Örnekleri</h2>
    <div align="center">
        <img src="https://github.com/yasir723/Agac-Elemanlari-Yazdirmak-Pre-Order/assets/111686779/294ca6ec-6a90-4838-89f8-6f56d1fea828" width="334">
        <img src="https://github.com/yasir723/Agac-Elemanlari-Yazdirmak-Pre-Order/assets/111686779/725aa740-c6b1-4f8d-97f8-e9a60d8eaffb" width="334">
        <img src="https://github.com/yasir723/Agac-Elemanlari-Yazdirmak-Pre-Order/assets/111686779/e25e9a6e-15b2-4815-84c5-3c29498ada75" width="334">
    </div>
</div>


Bu C# sınıfı, ağaç veri yapısını oluşturmak için kullanılır
## `tree` Sınıfı

```csharp
class tree
{
    public int value;
    public tree right;
    public tree left;
}
```

### Özellikler

- `value`: Düğümün değerini temsil eder.
- `right`: Düğüme bağlı olan sağ alt düğümü belirtir.
- `left`: Düğüme bağlı olan sol alt düğümü belirtir.

## `simetrikMi` Metodu
```csharp
static int simetrikMi(tree node1, tree node2)
{
    if (node1 == null && node2 == null) return 0;

    if (node1 == null || node2 == null) return 1;

    if (node1.value != node2.value) return 1; 

    return simetrikMi(node1.left, node2.right) + simetrikMi(node1.right, node2.left);
}
```

## Parametreler

- `node1`: Ağaçtaki mevcut düğüm.
- `node2`: Aynı ağaçtaki mevcut düğümü bir daha göndermek.

## Dönüş Değeri

Bu metodun dönüş değeri bir tamsayıdır (integer). `Eğer döndürülen değer 0 ise, verilen ağaç simetriktir. Ancak 0'dan büyük bir değer döndürülüyorsa, ağaç simetrik değildir`. Bu algoritmada, simetrik olmasına aykırı her bir düğüm için 1 döndürülür. En sonunda, recursive olarak çağırıldığında her iki çağrı arasında + işareti yazıldığı için döndürülen tüm değerler toplanarak dönüş değeri oluşturulur. Örneğin, 0 + 0 + 0 + 1 + 1 + 1 + 0 + 0 gibi bir durum oluşabilir. Dolayısıyla, `döndürülen değer sıfırdan büyük olabilir`.

## Avantaj

- İki ağaç birbirine simetrik olup olmadığını kontrol etmeyi sağlar.
- Aynı ağacı hem node1 hem de node2 olarak göndererek, bu ağacın kendisine simetrik olup olmadığını kontrol etmeyi sağlar.

## İşleyiş

1. İlk olarak, iki düğüm de null ise (her iki ağaç da boş), simetrik olarak kabul edilir ve 0 döndürülür.
2. Eğer yalnızca bir düğüm null ise, bu durumda ağaçlar simetrik değildir ve 1 döndürülür.
3. Bu iki if komutu geçtikten sonra demek her iki düğüm de null değildir.
4. Eğer her iki düğüm de null değilse, düğümlerin değerleri karşılaştırılır. Eğer değerler eşit değilse, ağaçlar simetrik değildir ve 1 döndürülür.
5. Eğer düğümlerin değerleri eşit ise, simetriklik kontrolü için her iki ağacın alt ağaçlarına da aynı anda rekürsif olarak bakılır. Sol ağacın sol alt ağacı ile sağ ağacın sağ alt ağacı karşılaştırılır ve sol ağacın sağ alt ağacı ile sağ ağacın sol alt ağacı karşılaştırılır. Bu işlem toplamda iki alt ağacın simetrikliğini kontrol eder.
6. Son olarak, bu rekürsif çağrıların sonuçları toplanır ve döndürülür. Eğer toplam değer 0 ise, ağaçlar simetrik olarak kabul edilir.

## `Main` Metodu
```csharp
static void Main(string[] args)
{
    // Ağaç yapısını oluşturma
    tree root = new tree() { value = 9 };
    root.left = new tree() { value = 7 };
    root.right = new tree() { value = 7 };
    root.left.left = new tree() { value = 3 };
    root.left.right = new tree() { value = 2 };
    root.right.left = new tree() { value = 2 };
    root.right.right = new tree() { value = 3 };

    // simetrik metodu kullanımı
    if (simetrikMi(root, root) == 0)
        Console.WriteLine("simetriktir");
    else
        Console.WriteLine("simetrik değildir");

    Console.ReadKey();
}
```
## çıktı 
```cmd
simetriktir
```

<div align="center">
    <h3>Simetrik Bir Ağaç Metot Çalışma Adımları</h3>
</div>

[![Simetrik Kontrolü](https://github.com/yasir723/Simetrik-Agac/assets/111686779/1a79253b-4735-4f53-a7c8-825a9c28f6a3)](https://github.com/yasir723/Simetrik-Agac/assets/111686779/1a79253b-4735-4f53-a7c8-825a9c28f6a3)


Yukarıdaki örnekte metot 0 değeri döndürdü, bu da verilen ağacın simetrik olduğunu gösterir


<div align="center">
    <h3>Simetrik Olmayan Bir Ağaç Metot Çalışma Adımları</h3>
</div>

[![Simetrik Kontrolü](https://github.com/yasir723/Simetrik-Agac/assets/111686779/4b202f62-0ee7-4c22-9e84-5654cc60499e)](https://github.com/yasir723/Simetrik-Agac/assets/111686779/4b202f62-0ee7-4c22-9e84-5654cc60499e)


Yukarıdaki örnekte metot 2 değeri döndürdü, sıfırdan büyük olduğundan verilen ağacın simetrik olmadığını gösterir

