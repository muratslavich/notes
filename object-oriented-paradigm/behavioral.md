# [Design patterns](patterns.md)
## Behavioral patterns
###	Chain of Responsibility
<details>
	<summary>Request along a chain of handlers</summary>

![](chain.png)  

```java
interface HeadersChain {
    fun addHeader(inputHeader: String): String
}

class AuthenticationHeader(
    val token: String?,
    var next: HeadersChain? = null
) : HeadersChain {
    override fun addHeader(inputHeader: String): String {
        token ?: throw IllegalStateException("Token should be not null")
        return inputHeader + "Authorization: Bearer $token\n".let { next?.addHeader(it) ?: it }
    } // execute chain by execute next.method()
}

class ContentTypeHeader(
    val contentType: String,
    var next: HeadersChain? = null
) : HeadersChain {
    override fun addHeader(inputHeader: String): String =
        inputHeader + "ContentType: $contentType\n".let { next?.addHeader(it) ?: it }
}

class BodyPayload(
    val body: String,
    var next: HeadersChain? = null
) : HeadersChain {
    override fun addHeader(inputHeader: String): String =
        inputHeader + body.let { next?.addHeader(it) ?: it }
}

class ChainOfResponsibilityTest {

    @Test
    fun `Chain Of Responsibility`() {
        //create chain elements
        val authenticationHeader = AuthenticationHeader("123456")
        val contentTypeHeader = ContentTypeHeader("json")
        val messageBody = BodyPayload("Body:\n{\n\"username\"=\"dbacinski\"\n}")

        //construct chain
        authenticationHeader.next = contentTypeHeader
        contentTypeHeader.next = messageBody

        //execute chain
        val messageWithAuthentication =
            authenticationHeader.addHeader("Headers with Authentication:\n")

        println(messageWithAuthentication)

        val messageWithoutAuth =
            contentTypeHeader.addHeader("Headers:\n")
        println(messageWithoutAuth)

        assertThat(messageWithAuthentication).isEqualTo(
            """
                Headers with Authentication:
                Authorization: Bearer 123456
                ContentType: json
                Body:
                {
                "username"="dbacinski"
                }
            """.trimIndent()
        )

        assertThat(messageWithoutAuth).isEqualTo(
            """
                Headers:
                ContentType: json
                Body:
                {
                "username"="dbacinski"
                }
            """.trimIndent()
        )
    }
}
```

</details>

### Command
<details>
	<summary>Turn a request into a stand-alone object that contains all information about the request</summary>

![](command.png)

```java
interface OrderCommand {
    fun execute()
}

class OrderAddCommand(private val id: Long) : OrderCommand {
    override fun execute() = println("Adding order with id: $id")
}

class OrderPayCommand(private val id: Long) : OrderCommand {
    override fun execute() = println("Paying for order with id: $id")
}

class CommandProcessor {

    private val queue = ArrayList<OrderCommand>()

    fun addToQueue(orderCommand: OrderCommand): CommandProcessor =
        apply {
            queue.add(orderCommand)
        }

    fun processCommands(): CommandProcessor =
        apply {
            queue.forEach { it.execute() }
            queue.clear()
        }
}

class CommandTest {

    @Test
    fun command() {
        CommandProcessor()
            .addToQueue(OrderAddCommand(1L))
            .addToQueue(OrderAddCommand(2L))
            .addToQueue(OrderPayCommand(2L))
            .addToQueue(OrderPayCommand(1L))
            .processCommands()
    }
}
```

</details>

### Mediator
<details>
	<summary>Restrict direct communications between the objects and forces them to collaborate only via a mediator object</summary>

![](mediator.png)

```java
class ChatUser(private val mediator: ChatMediator, private val name: String) {
    fun send(msg: String) {
        println("$name: Sending Message= $msg")
        mediator.sendMessage(msg, this)
    }

    fun receive(msg: String) {
        println("$name: Message received: $msg")
    }
}

class ChatMediator {

    private val users: MutableList<ChatUser> = ArrayList()

    fun sendMessage(msg: String, user: ChatUser) {
        users
            .filter { it != user }
            .forEach {
                it.receive(msg)
            }
    }

    fun addUser(user: ChatUser): ChatMediator =
        apply { users.add(user) }

}

class MediatorTest {

    @Test
    fun Mediator() {
        val mediator = ChatMediator()

        val john = ChatUser(mediator, "John")

        mediator
            .addUser(ChatUser(mediator, "Alice"))
            .addUser(ChatUser(mediator, "Bob"))
            .addUser(john)

        john.send("Hi everyone!")
    }
}
```

</details>

### Memento
<details>
	<summary>Save and restore the previous state of an object without revealing the details of its implementation</summary>

![](memento.png)

</details>

### Observer
<details>
	<summary>Define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing</summary>

![](observer.png)

```java
interface EventListener {
    fun update(eventType: String, file: File)
}

class EmailNotificationListener(private val email: String) : EventListener {
    override fun update(eventType: String, file: File) {
        println("Email to  $email: Someone has performed $eventType operation with the following file: ${file.name}")
    }
}

class LogOpenListener(fileName: String) : EventListener {
    private val log = File(fileName)

    override fun update(eventType: String, file: File) {
        println("Save to log $log: Someone has performed $eventType operation with the following file: ${file.name}")
    }
}

class EventManager(vararg operations: String) {
    private val listeners: HashMap<String, MutableList<EventListener>> = HashMap()

    init {
        operations.forEach { listeners[it] = mutableListOf() }
    }

    fun subscribe(eventType: String, listener: EventListener) = listeners[eventType]?.add(listener)
    fun unsubscribe(eventType: String, listener: EventListener) = listeners[eventType]?.remove(listener)
    fun notify(eventType: String, file: File) = listeners[eventType]?.forEach { it.update(eventType, file) }
}

class Editor {
    val events = EventManager("open", "save")
    private var file: File? = null

    fun openFile(filePath: String) {
        file = File(filePath)
        events.notify("open", file!!)
    }

    fun saveFile() {
        events.notify("save", file!!)
    }
}

fun main() {
    val editor = Editor()
    editor.events.subscribe("open", LogOpenListener("/path/to/log/file.txt"))
    editor.events.subscribe("save", EmailNotificationListener("admin@example.com"))

    editor.openFile("test.txt")
    editor.saveFile()
}
```

</details>

##### State
<details>
	<summary>code</summary>		
</details>

##### Strategy
<details>
	<summary>code</summary>		
</details>

##### Template Method
<details>
	<summary>code</summary>		
</details>

##### Visitor
<details>
	<summary>code</summary>		
</details>
