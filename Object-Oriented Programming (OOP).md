##### Object-Oriented Programming (OOP)
แนวคิดหรือรูปแบบ (paradigm) ในการเขียนและออกแบบโปรแกรม โดยมองภาพเป็นวัตถุ(Objects) แทนที่จะเป็นลำดับของคำสั่ง (แบบ Procedural Programming)

OOP ทุกสิ่งในโปรแกรมจะถูกมองว่าเป็นวัตถุ ซึ่งเป็นเสมือน "สิ่งของ" (Object) ที่มี
	- ข้อมูล(Data หรือ Attributes/Properties/state): ลักษณะเฉพาะของวัตถุ เช่น สี, ขนาด, ชื่อ
	- ฤติกรรม(Behavior หรือ Methods/Functions): สิ่งที่วัตถุนั้นสามารถทำได้ หรือการกระทำที่สามารถเกิดขึ้นกับวัตถุนั้นได้ เช่น การเดิน, การส่งเสียง, การคำนวณ

**ทำไมต้อง OOP**
	ปัญหา: *หากย้อนกลับไปก่อนมี OOP การพัฒนาซอฟต์แวร์ใช้แนวคิด Procedural Programming (การเขียนโค้ดตามลำดับขั้นตอน) เมื่อระบบหรือซอฟต์แวร์มีขนาดใหญ่หรือซับซ้อนมากขึ้น ก็จะเกิดปัญหาหลายๆอย่างเกิดขึ้น เช่น*
	
	- ข้อมูลกระจัดกระจาย (data เดียวกันแต่กระจายไปหลายที่ใน code)
	- ควบคุมการเข้าถึงข้อมูลได่้ยาก
	- ยากต่อการทำความเข้าใจภาพรวม และเมื่อแก้โค้ดส่วนหนึ่ง อาจส่งผลกระทบต่อส่วนอื่นโดยไม่ตั้งใจ
	- โค้ดซ้ำซ้อน
	- ดูแลและแก้ไขได้ยาก เมื่อซอฟต์แวร์มีขนาดใหญ่หรือซับซ้อน
	- ยากต่อการ reuse

**4 เสาหลักของ OOP**

> - **Encapsulation (การห่อหุ้มข้อมูล)**

	- ซ่อนรายละเอียดภายใน object
	- จำกัดการเข้าถึงข้อมูลบางส่วนจากภายนอก
	- ป้องกันข้อมูลถูกแก้ไขโดยไม่ตั้งใจจากภายนอก

``` Javascript
class Car {
	constructor(model) {
		this.model = model;
		this.speed = 0;
	}
	accelerate(amount) {
		this.speed += amount;
	}
	getCurrentSpeed() {
		return this.speed;
	}
}
const car = new Car('Jazz');
car.accelerate(50);
// car.speed error // ไม่ควรเข้าถึงโดยตรงแบบนี้
console.log(`Current speed: ${car.getCurrentSpeed()} km/h`);
// Current speed: 50 km/h
```

> - **Inheritance (การสืบทอด)*

	- reuse และขยาย class
	- สร้าง class ใหม่จาก class เดิม (แม่ Superclass -> ลูก Subclass)
	- ได้รับคุณสมบัติ (Properties) และพฤติกรรม (Methods) ทั้งหมดของคลาสเดิม
	- นำโค้ดกลับมาใช้ใหม่ (Code Reusability)
	- ทำให้ลดความซ้ำซ้อน

``` Javascript
class Car {
	contructor(model) {
		this.model = model;
		this.speed = 0;
	}
	accelerate(amount) {
		this.speed += amount;
	}
}

class Honda extends Car { // SupClass
	constructor(model, engine) {
		supper(model); //call constructor SuperClass
		this.engine = engine;
	}
	foldAllSeat() {
		return 'All seat folded.';
	}
}

const jazz = new Honda('Jazz', 'Gasoline');
jazz.accelerate(50); // สืบทอดจากคลาสแม่
jazz.foldAllSeat(); // method เฉพาะของคลาสลูก
// *ได้คุณสมบัติของ accelerate มาจากคลาสแม่ ไม่จำเป็นต้อง implement ซ้ำ
```

> - **Polymorphism (ความหลากหลายทางรูปร่าง)**

	-เขียนโค้ดที่ flexible และ extensible
	- การใช้ Interface ในการสั่งงานวัตถุหลายชนิด แต่ละชนิดจะแสดงพฤติกรรมที่แตกต่างกันไป
	- ทำให้โค้ดยืดหยุ่นและขยายระบบได้ง่าย (Extensibility)

``` Javascript
class Animal () {
	constructor(name) {
		this.name = name;
	}
	makeSound() {
		return ''
	}
}

class Dog extends Animal {
	constructor(name) {
		super(name);
	}
	makeSound() { // เขียนทับ makeSound ของคลาสแม่
		return `${this.name} เห่า: โฮ่งๆ`;
	}
}
class Cat extends Animal { 
	constructor(name) { 
		super(name); 
	} 
	makeSound() { // เขียนทับ makeSound ของคลาสแม่
		return `${this.name} ร้อง: เหมียวๆ`;
	}
}
// *ทั้งหมาและแมวเป็นสัตว์ ที่ส่งเสียงได้เหมือนกัน แต่เสียงต่างกัน
```

> - **Abstraction (นามธรรม)**

	- โฟกัสเฉพาะสิ่งสำคัญ แสดงข้อมูลหรือฟังก์ชันที่จำเป็นต่อการใช้งาน ซ่อนความซับซ้อนที่ไม่เกี่ยวข้องไว้
	- ไม่จำเป็นต้องรู้ว่าเบื้องหลังทำงานรู้วิธีแค่เรียกใช้งานก็พอ มักทำผ่าน Abstract Class/Interface
	- ลดความซับซ้อนในการใช้งานและการทำความเข้าใจระบบ

``` Typescript
abstract class Shape {
	protected color: string;
	constructor(color) {
		this.color = color;
	}
	// เมธอดนามธรรม (Abstract Method) 
	// ไม่มี implementation คลาสลูกต้องเขียนทับ
	abstract calculateArea(): number;
}
class Circle extends Shape {
	constructor(color: string, radius: number) {
		super(color);
	}
	calculateArea(): number { // บังคับ implement ตามคลาสแม่
		return Math.PI * radius * radius;
	}
}
class Ractagle extends Shap {
	constructor(color: string, width: number, hieght) {
		super(color);
	}
	calculateArea(): number { // บังคับ implement ตามคลาสแม่
		return this.width * this.hieght;
	}
}
```

``` Typescript
interface User {
	create(user: User): void; // ไม่มี implementation บอกแค่อยากได้อะไร รีเทิร์นอะไร
	getAll(): Array<User>; // ไม่มี implementation
}

class UserImpl implement User {
	create(user: User): void { // บังคับ implement ตามคลาสแม่
		//implementation such as storage to db
	}
	getAll(): void { // บังคับ implement ตามคลาสแม่
		return [{/* user */}] // list of user
	}
}
```

OOP ถูกสร้างขึ้นเพื่อช่วยจัดการกับความซับซ้อนของซอฟต์แวร์ขนาดใหญ่ ทำให้โค้ดสามารถนำกลับมาใช้ใหม่ได้ง่ายขึ้น บำรุงรักษาและแก้ไขได้สะดวกขึ้น และช่วยให้นักพัฒนาสามารถสร้างโมเดลของปัญหาจากโลกจริงให้อยู่ในรูปแบบของโค้ดได้อย่างเป็นธรรมชาติมากขึ้น