# Java Inner Sınıflar

**Inner** ya da **Nested** sınıflar, **interfaceler** ya da sınıfların içerisinde yer alabilir. İşlemleri mantıksal gruplara ayırmaya yarar. Bu okunabilirliği arttırır, bakımı kolaylaştırır.

**Static olmayan inner** sınıflara **inner** sınıflar denir. Bir inner sınıf üst sınıfın private dahil tüm metodlarına ve değişkenlerine erişebilir. **Static olan inner** sınıflara **Nested Class** denir.

```java
class A {

    private String var = "Variable";

    class InnerClass {
        
        void func() {
            System.out.println(var);
        }
    }
}
```

### Inner Sınıflar

Inner Sınıflar 3’e ayrılır:

* **Member Inner Class**: Üye iç sınıf olarak bilinir. Üst sınıfın değişkenlerine erişebilen ve sınıfın içerisinde tanımlanmış olan iç sınıftır.

```java
class A {
    private String var = "Variable";

    private void func1() {
        System.out.print(var);
    }

    class InnerClass {

        void func2() {
            func1();
            System.out.println(var);
        }
    }
}
```

* **Anonymous Inner Class**: Anonim iç sınıflardır. Bir **interface ya da abstract sınıfı** implemente etmeden **new** anahtar kelimesi ile direk olarak kullanabiliriz. Fakat metotları **inner sınıf** içerisinde **implemente** etmek koşuluyla. Burada aslında **interfacenin** bir örneği oluşturulmaz. Burada oluşan şey **anonim sınıfın** bir örneğidir ve interface içindeki fonksiyonları **override** etmek gereklidir. **Java 8** ile birlikte bu işleme gerek kalmadan **lambda expression ve functional interfaceler** kullanarak aynı işlemi kısa ve daha kolay bir şekilde halledebiliyoruz.

```java

interface A {

    public void func1();

    public void func2();
}

class Test {
    public static void main(String args[]) {

        A anonymousInstance = new A() {
            @Override
            public void func1() {
                System.out.println("Function 1");
            }

            @Override
            public void func2() {
                System.out.println("Function 2");
            }
        };

        anonymousInstance.func1();
        anonymousInstance.func2();
    }
}
```
* **Local Inner Class**: Bu sınıflar metot içerisinde oluşturulan sınıflara verilen addır. Private, public ya da protected olamazlar. Metodun dışından erişilemezler, yaşam süreleri metot boyuncadır. **Java 1.7** ye kadar local inner sınıfın, metot içindeki değişkenlere erişebilmesi için o değişkenin private olması gerekliydi.

```java
class A {
    public void func1() {
        String var = "Variable";

        class LocalInnerClass {
            void func() {
                System.out.println(var);
            }
        }

        LocalInnerClass localInstance = new LocalInnerClass();
        localInstance.func();
    }
}
```

### Static Inner Sınıflar(Nested Sınıflar)

Bu sınıflar üst sınıfın **static** olmayan değişken ve metotlarına direkt erişemezler. Dış sınıfın ismiyle birlikte bu sınıflara erişim mümkündür. Eğer static iç sınıfın içerisinde statik bir değişken ya da metot varsa bunlara nesne oluşturmadan erişmek mümkündür.

```java
class A {

    private String var1 = "Variable 1";
    static private String staticVariable = "Variable 2";

    static class NestedClass {
        public static void staticFunction() {
            System.out.println(staticVariable);

            A a = new A();
            System.out.println(a.var1);
        }

        public void func() {
            System.out.println(staticVariable);

            A a = new A();
            System.out.println(a.var1);
        }
    }
}

class Test {
    public static void main(String args[]) {
        A.NestedClass.staticFunction();

        A.NestedClass a = new A.NestedClass();
        a.func();
    }
}
```

### Nested Interface

**Sınıfın** ya da **interfacenin** içerisinde bir **iç interface** yaratmak mümkündür. Bunlarda gruplandırma yapmak için kullanılırlar ve bakımı kolaylaştırırlar.

```java
interface A {

    public void functionA();

    interface NestedInterface {
        public void nestedFunction();
    }
}

class B implements A.NestedInterface {

    @Override
    public void nestedFunction() {
        System.out.println("Nested Interface Function Implement");
    }
    
    interface NestedInterface{
        void nestedFunction();
    }
}

class C implements B.NestedInterface{

    @Override
    public void nestedFunction() {
        System.out.println("Nested Interface Function Implement");
    }
}
```
