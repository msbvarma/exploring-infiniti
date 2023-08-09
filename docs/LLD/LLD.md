# LLD Cohort - 2023
Welcome Folks :)

* Chess
* Parking Lot
* Cab booking.
* Movie Ticket Booking
* enginEBogie.

# 👉 What is Low-Level Design, their formats, and expectations from the interviewers?

- What it is?
* Single Service
	* Parking Lot
		ParkingLot
		Slot
		Vehicle

- Formats
	* F2F - Face to face
		* 60 mins.
		* You will get a problem
		* You will come up with classes/properties of them.
		* You will code few core areas of the classes.
	
	* Machine Round
		* Generally 2-2.5 hrs.
		* You have code the full solution.
		* Extensibility.

- Interviewer Expectations
* Ask the interview what they are expecting.

* Goals
	* Maintainability
	* Extensibility
	* Readable
	* Testability - Unit testing.
* Non Goals
	* Scalability - Number of users.
	* Using external systems - Redis, db.
		* How can you switch between them easily.
	* Complex implementation - 
		* Algo to be used.
			* Parking lot - Algorithm to be used for allocation
				* Iterate over a list - O(n)
				* Random Function - O(1)
		* List or map.
	* Concurrency.


# 👉 Difference between principles and patterns

* Principles - SOLID
* Patterns - Strategy, Composite, Factory, etc.

# 👉 When should you use principles and when should you use patterns?

* When Principles?
	- Guidance/Guidelines.
	- Rules
	- Analogy: We should be helpful beings.
	- Useful for analysis.

* When Patterns?
	- Something like templates.
	- Defines way the objects need to behave.
	- How you can achieve those rules.


# 👉 SOLID Principles

S - SRP
O - OCP
L - LSP
I - ISP
D - DIP

#### 👨‍💻 Single Responsibility.

- Definition: 
	+ Single? One class should have single responsility.
	+ Single reason to change.
	+ 



Examples:

* Parking Lot
```java

class SlotsManager {
	List<Slot> slots;
}

class ParkingLot {
	List<Slot> slots;

	slots management
	vehicke management
	tickeeting management
}

class TicketService {

}

===============
class SlotsManager {
	List<CarSlot> carSlots;
	List<TruckSlot> truckSlots;
}

class TicketingService {

}

class ParkingLot {

	SlotsManager slotsManager;
	TicketingServicetTicketingService;
}

```

* User Model Class
```java
class User {
	String id;
	String name;
	String address;
	String paymentMethods;
	String email;
}
```

```java
class Address {
	String city;
	String id;
	String state;
	String country;
}

class PaymentMethod {
	String id;
	Sttring type;
	String cardName;
	String walletName;
}

class User {
	String id;
	String name;

	String country;

	List<PaymentMethod> paymentMethods;
	String email;
}
```

#### 👨‍💻 OCP - Open Closed Principle
* ? Open for extension and closed modification. - For any new case
	* class?
	* interface?
	* method?
? =-> Any piece of code.
* Less modifications for the existing classes.
* Less number of test cases will be modified.

* Why:
	* Less number of test cases will be modified.
		* More testing effort
	* We always create mistakes. We dont want to modify existing code.
	* Not all the times, you have liberty to change it.


* Not allowed to change
```java
List<String> = new ArrayList<>();

class List {
	String[] strings;	
	size
	delete
}

class Integer {
	Integer[] integer;	
	size
	delete
}

```

```java

// Key-Value -> String
// Eviction
class Cache {
	// Max 100 elements

	Map<Object, Object> elements;
	LRUEvictionPolicy lruEvictionPolicy;

	Object get(Object key) {
		return elements.get(key);
	}

	Object put(Object key, Object value) {
		if (elements.size() > 100) {
			Object elementKey = lruEvictionPolicy.getElementToRemove();
			elements.remove(elementKey);
		}
		elements.put(key, value);
	}
}

interface IEvictionPolicy {
	String getElementToRemove();
}

class LRUEvictionPolicy implements IEvictionPolicy {
	String getElementToRemove() {

	}
}

interface IStore {
	String store(String key, Stirng value);
	String get(String key);
}

class LRUEvictionPolicy implements IEvictionPolicy {
	String getElementToRemove() {

	}
}

class CacheItem {

}

class StringItem extends CacheItem {

}

class IntegerItem extends CacheItem {
	
}

class Cache<K, V> {
	int maxSize;

	//Map<K, V> elements;
	IStore store;
	IEvictionPolicy lruEvictionPolicy;

	Cache<K, V>(int maxSize) {
		this.maxSize = maxSize;
	}

	CacheItem get(String key) {
		return elements.get(key);
	}

	V get(K key) {
		return elements.get(key);
	}

	V put(K key, V value) {
		if (elements.size() > maxSize) {
			V elementKey = lruEvictionPolicy.getElementToRemove();
			elements.remove(elementKey);
		}
		elements.put(key, value);
	}
}

```
New problems in future.
* Instead of string data type, it could be something else.
* Cache size.
* Eviction policy
* What if I dont want to store the data in the map.



#### 👨‍💻 Liskov Substitution principle.
* A superclass should be usable wherever a subclass is needed.
* This principle is all about invariants.


```java

class Order {
	processOrder(orderItem);
}


class VideoBookingOrder extends Order {
	processOrder(orderItem) {
		// Validate
		// create a db entry
	}
}

class EventOrder extends Order {
	processOrder(orderItem) {
		// Validate
		// create a db entry
	}	
}

class CourseOrder extends Order {
	processOrder(orderItem) {

		// create a db entry
	}	
}


abstract class CacheItem {
	abstract equals();
	abstract hash();
}

interface ICacheKey {
	equals();
	hash();
}

interface IHashable {

}

interface IEQualable {

}

interface ICacheValue {
}


interface ICacheItem {
	equals();
	hash();
}

class StringItem extends CacheItem {

}

class IntegerItem extends CacheItem {
	
}

class UserItem extends CacheItem {
	equals();
	hash(){
		// Network
		// Not needed.
		return null;
	}

	dp {

	}

	profileUrl {

	}
}

class Cache {
	int maxSize;

	//Map<K, V> elements;
	Map<CacheItem, CacheItem> elements;
	LRUEvictionPolicy lruEvictionPolicy;

	Cache(int maxSize) {
		this.maxSize = maxSize;
	}

	CacheItem get(String key) {
		return elements.get(key);
	}

	CacheItem get(ICacheItem key) {
		return elements.get(key);
	}

	CacheItem put(CacheItem key, CacheItem value) {
		if (elements.size() > maxSize) {
			CacheItem elementKey = lruEvictionPolicy.getElementToRemove();
			elements.remove(elementKey);
		}
		elements.put(key, value);
	}
}




```

#### 👨‍💻 Interface Seggregation Principle
* A single contract/interface(top level item) should not be overloaded.

Cache
```java
abstract class CacheItem {
	abstract equals();
	abstract hash();
}

interface ICacheKey {
	equals();
	hash();
}

interface IHashable {

}

interface IEQualable {

}

interface ICacheValue {
}


interface ICacheItem {
	equals();
	hash();
}

class StringItem extends CacheItem {

}

class IntegerItem extends CacheItem {
	
}

class User extends CacheItem {
	equals();
	hash(){
		// Not needed.
		return null;
	}
}

class Cache {
	int maxSize;

	//Map<K, V> elements;
	Map<CacheItem, CacheItem> elements;
	LRUEvictionPolicy lruEvictionPolicy;

	Cache(int maxSize) {
		this.maxSize = maxSize;
	}

	CacheItem get(String key) {
		return elements.get(key);
	}

	CacheItem get(CacheItem key) {
		return elements.get(key);
	}

	CacheItem put(CacheItem key, CacheItem value) {
		if (elements.size() > maxSize) {
			CacheItem elementKey = lruEvictionPolicy.getElementToRemove();
			elements.remove(elementKey);
		}
		elements.put(key, value);
	}
}


interface IAccount {
	withdraw();
	deposit();
	mature();
}

interface IWithdrawalable {

}

interface CreditCard implements IWithdrawalable, {

}


interface Wallet implements IWithdrawalable, {

}

interface SavingsAccount implements IWithdrawalable, {

}

interface CurrentAccount implements IAccount {

}

interface FixedDepositAccount implements IAccount {

}


```

#### 👨‍💻 Dependency Inversion Principle
* Class should depend on an interface rather than concrete classes.
* High and low level components depend on abstractions.
* High level modules shouldn't depend on low-level modules.

```java
class Cache {
	int maxSize;

	//Map<K, V> elements;
	Map<CacheItem, CacheItem> elements;
	LRUEvictionPolicy lruEvictionPolicy;

	Cache(int maxSize) {
		this.maxSize = maxSize;
	}

	CacheItem get(String key) {
		return elements.get(key);
	}

	CacheItem get(CacheItem key) {
		return elements.get(key);
	}

	CacheItem put(CacheItem key, CacheItem value) {
		if (elements.size() > maxSize) {
			CacheItem elementKey = lruEvictionPolicy.getElementToRemove();
			elements.remove(elementKey);
		}
		elements.put(key, value);
	}
}

class LRUEvictionPolicy {
	List<String> list;
}


===

ISubscriber {
	processNewItem();
}

class PubSubQueue {
	Logger logger;
	Analytics analytics;

	publish(item) {
		logger.publish(item);
		analytics.publish(item);
	}
}


class PubSubQueueV1 {
	List<ISubscriber> subscribers;

	publish(item) {
		for (ISubscriber subscriber: subscribers) {
				subscriber.processNewItem(item);
		}
	}
}

```
