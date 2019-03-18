### Kelas-kelas
Alasan mengapa penting untuk memilki kelas dalam JavaScript sebagai item kelas pertama adalah:
1. [Kelas menawarkan abstraksi struktural yang berguna](./tips/classesAreUseful.md)
1. Menyediakan cara yang konsisten bagi pengembang untuk menggunakan kelas seperti framework (emberjs, reactjs dll) datang dengan versi mereka sendiri.
1. Pengembang-pengembang Object Oriented telah memahami kelas.

Akhirnya pengembangan JavaScript dapat *memiliki `class`*. Di sini kita memiliki kelas dasar yang disebut Point:
```ts
class Point {
    x: number;
    y: number;
    constructor(x: number, y: number) {
        this.x = x;
        this.y = y;
    }
    add(point: Point) {
        return new Point(this.x + point.x, this.y + point.y);
    }
}

var p1 = new Point(0, 10);
var p2 = new Point(10, 20);
var p3 = p1.add(p2); // {x:10,y:30}
```
Kelas ini menghasilkan JavaScript berikut pada ES5 emit:
```ts
var Point = (function () {
    function Point(x, y) {
        this.x = x;
        this.y = y;
    }
    Point.prototype.add = function (point) {
        return new Point(this.x + point.x, this.y + point.y);
    };
    return Point;
})();
```
Ini adalah pola kelas JavaScript tradisional yang cukup idiomatik sekarang sebagai konstruksi bahasa kelas satu.
 

### Inheritance
Kelas dalam TypeScript (seperti bahasa yang lain) mendukung *single* inheritance menggunakan perintah `extends` seperti yang ditunjukan di bawah ini:

```ts
class Point3D extends Point {
    z: number;
    constructor(x: number, y: number, z: number) {
        super(x, y);
        this.z = z;
    }
    add(point: Point3D) {
        var point2D = super.add(point);
        return new Point3D(point2D.x, point2D.y, this.z + point.z);
    }
}
```
Jika Anda memiliki konstruktor di kelas Anda maka Anda *harus* memanggil konstruktor induk dari konstruktor Anda (TypeScript akan menunjukan ini kepada Anda). Ini memastikan bahwa hal-hal yang perlu diatur pada gets set `ini`.   'If you have a constructor in your class then you *must* call the parent constructor from your constructor (TypeScript will point this out to you). This ensures that the stuff that it needs to set on `this` gets set. Diikuti oleh panggilan ke `super` Anda dapat menambahkan hal-hal tambahan yang ingin Anda lakukan di konstruktor Anda (di sini kami menambahkan anggota lain yaitu `z`).

Perhatikan bahwa Anda menimpa fungsi anggota orang tua dengan mudah (di sini kita menimpa `add`) dan masih menggunakan fungsionalitas kelas super di anggota Anda (menggunakan syntax `super.` ).

### Statics
Kelas-kelas TypeScript mendukung properti `static` yang dibagikan oleh semua instance kelas. properties that are shared by all instances of the class. A natural place to put (and access) them is on the class itself and that is what TypeScript does:

```ts
class Something {
    static instances = 0;
    constructor() {
        Something.instances++;
    }
}

var s1 = new Something();
var s2 = new Something();
console.log(Something.instances); // 2
```

You can have static members as well as static functions.

### Access Modifiers
TypeScript mendukung access modifiers `public`,`private` and `protected` yang menentukan aksesibilitas anggota `class` seperti yang ditunjukkan di bawah ini:

| accessible on   | `public` | `protected` | `private` |
|-----------------|----------|-------------|-----------|
| class           | yes      | yes         | yes       |
| class children  | yes      | yes         | no        |
| class instances | yes      | no          | no        |


If an access modifier is not specified it is implicitly `public` as that matches the *convenient* nature of JavaScript 🌹.

Note that at runtime (in the generated JS) these have no significance but will give you compile time errors if you use them incorrectly. An example of each is shown below:

```ts
class FooBase {
    public x: number;
    private y: number;
    protected z: number;
}

// EFFECT ON INSTANCES
var foo = new FooBase();
foo.x; // okay
foo.y; // ERROR : private
foo.z; // ERROR : protected

// EFFECT ON CHILD CLASSES
class FooChild extends FooBase {
    constructor() {
      super();
        this.x; // okay
        this.y; // ERROR: private
        this.z; // okay
    }
}
```

As always these modifiers work for both member properties and member functions.

### Abstract
`abstract` can be thought of as an access modifier. We present it separately because opposed to the previously mentioned modifiers it can be on a `class` as well as any member of the class. Having an `abstract` modifier primarily means that such functionality *cannot be directly invoked* and a child class must provide the functionality.

* `abstract` **classes** cannot be directly instantiated. Instead the user must create some `class` that inherits from the `abstract class`.
* `abstract` **members** cannot be directly accessed and a child class must provide the functionality.

### Constructor is optional

The class does not need to have a constructor. e.g. the following is perfectly fine. 

```ts
class Foo {}
var foo = new Foo();
```

### Define using constructor

Having a member in a class and initializing it like below:

```ts
class Foo {
    x: number;
    constructor(x:number) {
        this.x = x;
    }
}
```
is such a common pattern that TypeScript provides a shorthand where you can prefix the member with an *access modifier* and it is automatically declared on the class and copied from the constructor. So the previous example can be re-written as (notice `public x:number`):

```ts
class Foo {
    constructor(public x:number) {
    }
}
```

### Property initializer
This is a nifty feature supported by TypeScript (from ES7 actually). You can initialize any member of the class outside the class constructor, useful to provide default (notice `members = []`)

```ts
class Foo {
    members = [];  // Initialize directly
    add(x) {
        this.members.push(x);
    }
}
```
