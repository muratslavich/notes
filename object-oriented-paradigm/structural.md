# [Design patterns](patterns.md)
## Structural patterns
### Adapter
<details>
	<summary>Allows objects with incompatible interfaces to collaborate</summary>
<p>

The adapter implements the interface of one object and wraps the other one.

![](/images/structure-object-adapter.png)

```java
open class CelsiusTemperature(
    override var temperature: Double
): Temperature

class FahrenheitTemperature(
    override var temperature: Double
): Temperature

class FahrenheitAdapter(
    private val celsiusTemperature: CelsiusTemperature
) {
    fun convertToFahrenheitTemperature(): FahrenheitTemperature = FahrenheitTemperature(
        ((BigDecimal.valueOf(celsiusTemperature.temperature)
            .setScale(2) * BigDecimal(9) / BigDecimal(5)) + BigDecimal(32))
            .toDouble()
    )
}
```

</p>  	
</details>

### Bridge
<details>
<summary>Split related classes into separate independent hierarchies</summary>
<p>

Abstraction - high order layer, delegate the work to implementation layer.

The abstraction object controls the appearance of the app, delegating the actual work to the linked implementation object. Different implementations are interchangeable as long as they follow a common interface, enabling the same GUI to work under Windows and Linux.

![](/images/structure-en-2x.png)

```java
// Implementation layer
interface Device {
    var isEnabled: Boolean
    var volume: Int
}

class Tv(override var isEnabled: Boolean = false, override var volume: Int = 0) : Device
class Radio(override var isEnabled: Boolean = true, override var volume: Int = 10) : Device

// Abstraction layer
class Remote(val device: Device) {

    fun togglePower() {
        device.isEnabled = !device.isEnabled
    }

    fun volumeUp() = run { device.volume += 10 }
    fun volumeDown() = run { device.volume -= 10 }

}


fun main() {
    val tv = Tv()
    val radio = Radio()

    val remote = Remote(tv) // this is Bridge (aggregation over inheritance)
    remote.togglePower()

    print("${tv.isEnabled} ${tv.volume}")
}
```
</p>
</details>

### Composite
<details>
<summary>Compose objects into tree structures and then work with these structures</summary>
<p>

![](/images/composite.png)

```java
// hierarchy
open class Equipment(open val price: Int, name: String)
class Processor: Equipment(1070, "structural.Composite.Processor")
class HardDrive: Equipment(250, "Hard")
class Memory: Equipment(280, "structural.Composite.Memory")

// composite
open class Composite(name: String): Equipment(0, name) {
    private val equipments = ArrayList<Equipment>()
    override val price: Int
        get() = equipments.map { it.price }.sum()

    fun add(equipment: Equipment) = apply { equipments.add(equipment) }
}

class PersonalComputer: Composite("PC")


fun main() {
    val pc = PersonalComputer()
        .add(Processor())
        .add(HardDrive())
        .add(Memory())

    print(pc.price)
}
```

</p>		
</details>

### Decorator
<details>
	<summary>Attach new behaviors to objects by placing these objects inside special wrapper</summary>

![](/images/decorator.png)

  <p>

```java
interface CoffeeMachine {
    fun makeSmallCoffee()
    fun makeLargeCoffee()
}

class NormalCoffeeMachine : CoffeeMachine {
    override fun makeSmallCoffee() = println("Normal small coffee")
    override fun makeLargeCoffee() = println("Normal large coffee")
}

class EnhancedCoffeeMachine(private val coffeeMachine: CoffeeMachine) : CoffeeMachine by coffeeMachine {

    override fun makeSmallCoffee() {
        println("Enhanced small coffee")
    }

    fun makeCoffeeWithMilk() {
        makeSmallCoffee()
        addMilk()
        println("Enhanced small coffee with milk")
    }

    private fun addMilk() {}
}

fun main() {
    val normalCoffeeMachine = NormalCoffeeMachine()
    val enhancedCoffeeMachine = EnhancedCoffeeMachine(normalCoffeeMachine)

    enhancedCoffeeMachine.makeSmallCoffee()
    enhancedCoffeeMachine.makeLargeCoffee()
    enhancedCoffeeMachine.makeCoffeeWithMilk()
}
```

  </p>		
</details>

### Facade
<details>
<summary>Provides a simplified interface to a library, a framework, or any other complex set of classes</summary>

![](/images/facade.png)

<p>

```java
class ComplexSystem(private val filePath: String) {
    private val cache: HashMap<String, String>

    init {
        println("reading data from $filePath")
        cache = HashMap()
    }

    fun store(key: String, payload: String) {
        cache[key] = payload
    }

    fun read(key: String): String = cache[key] ?: ""

    fun commit() = println("Storing cached data: $cache to file: $filePath")
}

data class User(var login: String)

class UserRepository {
    private val systemPreferences = ComplexSystem("/data/default.prefs")

    fun save(user: User) {
        systemPreferences.store("User_key", user.login)
        systemPreferences.commit()
    }

    fun findFirst(): User = User(systemPreferences.read("User_key"))
}

fun main() {
    val userRepository = UserRepository()
    val user = User("murat")
    userRepository.save(user)
    val result = userRepository.findFirst()

    println("$result")
}
```

</p>		
</details>

### Flyweight
<details>
	<summary>Sharing common parts of state between multiple objects instead of keeping all of the data in each object</summary>		

![](/images/flyweight.png)

```java
// This class contain part of tree describing. It isn`t unique for each tree
// so it extract to own abstraction with container
// It helps reduce tree abstraction
class TreeType(val name: String, val color: Int, val texture: String) {
    fun draw(canvas: String, x: Int, y: Int) = println("TreeType(name='$name', color=$color, texture='$texture')")
}

class TreeFactory {

    companion object {
        private val treeTypes = mutableListOf<TreeType>()

        fun getTreeType(name: String, color: Int, texture: String): TreeType =
            treeTypes.find { it.name == name && it.color == color && it.texture == texture }
                ?: treeTypes.plus(TreeType(name, color, texture)).last()
    }
}

class Tree(private val type: TreeType, private val x: Int, private val y: Int) {
    fun draw(canvas: String) {
        type.draw(canvas, x, y)
    }
}

class Forest {
    private val trees = mutableListOf<Tree>()

    fun plantTree(x: Int, y: Int, name: String, color: Int, texture: String) {
        val type = TreeFactory.getTreeType(name, color, texture)
        val tree = Tree(type, x, y)
        trees.add(tree)
    }

    fun draw(canvas: String) = trees.forEach{ it.draw(canvas) }
}

fun main() {
    val forest = Forest()

    forest.plantTree(1,2,"sosna", 1,"square")
    forest.plantTree(2,3,"bereza", 1,"square")

    forest.draw("canvas")
}
```

</details>

### Proxy
<details>
	<summary>Controls access to the original object allowing to perform</summary>

![](/images/proxy.png)

```java
interface ThirdPartyLib {
    fun listVideos(): String
    fun getVideoInfo(id: Int): String
    fun downloadVideo(id: Int): String
}

class ThirdPartyLibImpl : ThirdPartyLib {
    override fun listVideos() = "list"
    override fun getVideoInfo(id: Int) = "info"
    override fun downloadVideo(id: Int) = "download..."
}

class CachedLib(
    private val service: ThirdPartyLibImpl
) : ThirdPartyLib {

    private var listCache: String? = null
    private var videoCache: String? = null
    private var resetNeed: Boolean = false

    override fun listVideos(): String {
        if (listCache.isNullOrEmpty() or resetNeed) listCache = service.listVideos()
        return listCache ?: ""
    }

    override fun getVideoInfo(id: Int): String {
        if (videoCache.isNullOrEmpty() or resetNeed) videoCache = service.getVideoInfo(id)
        return videoCache ?: ""
    }

    override fun downloadVideo(id: Int): String {
        if (videoCache.isNullOrEmpty() or resetNeed) videoCache = service.downloadVideo(id)
        return videoCache ?: ""
    }
}

class Manager(private val lib: ThirdPartyLib) {
    fun renderVideo() = println(lib.getVideoInfo(1))
    fun renderList() = println(lib.downloadVideo(1))
}

fun main() {
    val service = ThirdPartyLibImpl()
    val proxy = CachedLib(service)

    val manager = Manager(proxy)
    manager.renderList()
    manager.renderVideo()
}
```

</details>
