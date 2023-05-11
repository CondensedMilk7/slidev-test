# რა არის Dependency Injection?

ფრიდონ თეთრაძე

---

# Dependencies
```ts
class Knight {
  defend() {
    return "defend the ruler";
  }
}
class General {
  command() {
    return "give commands";
  }
}
```

# Dependent

```ts
class Soldier {
  general: General;
  orders = "no orders for now";
  constructor() {
    this.general = new General();
    this.orders = this.general.command();
  }
}
```

---
layout: center
---

```ts {1-3|5|all}
const soldier1 = new Soldier();
const soldier2 = new Soldier();
const soldier3 = new Soldier();

console.log(soldier1.general === soldier2.general); // false
```

---

# უკეთესი გზა

### დეკლარაციის დროს

```ts {all|3|all}
class Soldier {
  orders = "no orders for now";
  constructor(public general: General) {
    this.orders = this.general.command();
  }
}
```

### შექმნის დროს

```ts {0|1-5|all|6}
const general = new General();
const soldier1 = new Soldier(general);
const soldier2 = new Soldier(general);
const soldier3 = new Soldier(general);

console.log(soldier1.general === soldier2.general); // true
```
---

# ბევრი Dependency

### დეკლარაციის დროს

```ts
class King {
  constructor(
    public knight: Knight,
    public general: General,
    public soldier: Soldier
  ) {}
}
```

### შექმნის დროს

```ts {0|1|1-2|1-3|all}
const knight = new Knight();
const general = new General();
const soldier = new Soldier(general);
const king = new King(knight, general, soldier);
```

---

# DI ანგულარში

- ანგულარს გააჩნია DI Container
- ის ჩვენ მაგივრად აწვდის კლასებს საჭირო dependecy-ებს
- ჩვენ უბრალოდ უნდა გამოვაცხადოთ Dependency-ები

---
layout: center
---

# შეკითხვები?