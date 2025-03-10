# Değişkenler, sabitler ve statik öğeler
⭐️ Rust programlama dilinde değişkenler aksi belirtilmediği sürece değişmez olarak kabul edildiğinden, değişken kavramıyla aslında **değişken bağlamı**na işaret edilir. Eğer bu bağlamın değişebilir olması isteniyorsa değişken bildirilirken `mut` anahtar sözcüğünün kullanılması gereklidir.

⭐️ Rust statik olarak tasarlanmış bir dil olduğundan, veri türlerini derleme zamanında kontrol eder. Bu nedenle değişken tanımlarında tür bildirimi zorunlu tutulmaz. Tür bildirilmediğinde derleyici, ifade ve kullanımı kontrol ederek en olası veri türünü belirlemeye çalışır. 
Bununla birlikte eğer **sabit** ya da **statik** bir bağlam tanımlanıyorsa o bağlamın türü mutlaka bildirilmek zorundadır. Türler `(:)` iki noktanın ardından bildirilir. 

### Değişken bağlama
Değişken ifade edilirken bağlayıcı olarak genellikle `let` anahtar sözcüğü kullanılır. Bu yolla programda kullanılan isimleri bir değer yada işleve bağlamak mümkün olur. 

```Rust
fn main() {
  let a = true; 
  println!("a: {}", a);
  
  let b: bool = false; 
  println!("b: {}", b);
  
  let (x, y) = (1, 5); 
  println!("x: {}, y: {}", x, y);
  
  let mut z = 5; 
  println!("z: {}", z);
  
  z = 6;
  println!("Şimdiki z: {}", b);
  
  let (mut e, mut f) = (-12, 20.1);
  println!("e: {}, f: {}", e, f);
  
  e = 9;
  f = 9.9;
  println!("Yeni e: {}, yeni f: {}", e, f);
}
````

Bağlayıcı ifadenin sol tarafı bir model olduğundan `let` anahtar sözcüğü yardımıyla çok sayıda isim bir dizi değere veya işlev değerine bağlanabilir.

```Rust
let (x, y, z ) = (1, 5, 10); 
  println!("x: {}, y: {}, z: {}", x, y, z);
````
Çoklu tanımlanan değişkenlerin ileride değiştirilmesi gerekiyorsa
```Rust
let (mut x, mut y,  mut z) = (1, 5, 10);
x += x; y += y; z += z;
println!("x:{}, y:{}, z:{}", x, y, z); // x:2, y:10, z:20
````
### Sabitler

Sabitleri tanımlamak için `const` anahtar sözcüğü kullanılır. Değişkenlerin aksine sabitler tanımlanırken türlerinin açıkça bildirilmesi gerekir. 
Program çalıştığı sürece yaşayan ve derleme esnasında değerleriyle yer değiştiren bu türlerin bellekte kalıcı adresleri bulunmadığından, kendilerine yapılan  başvuruların aynı hafıza adresine erişeceği garanti edilmez.

```Rust
fn main() {
  const S: i32 = 5;
  println!("S sabitinin değeri: {}," S);
}
````
Sabitler varsayılan olarak değil daima değişmez olduklarından, sabit bildirimlerinde `mut` anahtar kelimesi kullanılamaz.

### Statikler

Bir küresel değişken türü tanımımlanırken `static` anahtar sözcüğü kullanılır. Bu türler sabitlere benzemekle birlikte, bellekte üzerinde bir adresleri bulunur. Bu türlerin her değeri için sadece bir örnek olabilir ve bu örnekler kullanılırken satır içlerine alınmazlar.

```Rust
fn main() {
  static S: i32 = 10;
  println!("S global değeri: {}," S);
}
````
Statik öğeler genellikle kod dosyasının en üstünde işlevlerin dışında bulundurulurlar. Sabit türünün hafıza adresine nadiren başvurulduğundan, kodun eniyileştirilmesi için zorunlu olmadıkça statik tür yerine sabitlerin kullanılması yeğlenmelidir.
```Rust
static NAME: &'static str = "Apache";
print!("{}", NAME);
````
