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

##### Iterator
<details>
	<summary>code</summary>		
</details>

##### Mediator
<details>
	<summary>code</summary>		
</details>

##### Memento
<details>
	<summary>code</summary>		
</details>

##### Observer
<details>
	<summary>code</summary>		
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
