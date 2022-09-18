## RESTful API

### RESTful	Web	Services
REST stands for REpresentational State Transfer. REST is a web standards based architecture and uses HTTP Protocol for data communication. It revolves around resources where every component is a resource and a resource is accessed by a common interface using HTTP standard methods. REST was first introduced by Roy Fielding in year 2000.

In REST architecture, a REST Server simply provides access to resources and the REST client accesses and presents the resources. Here each resource is identified by URIs/ Global IDs. REST uses various representations to represent a resource like Text, JSON and XML. JSON is now the most popular format being used in Web Services.

RESTful Web Services are basically REST Architecture based Web Services. In REST Architecture everything is a resource. RESTful web services are light weight, highly scalable and maintainable and are very commonly used to create APIs for web-based applications.

### REST Features
-	Resource
-	Messages
-	Addressing
-	Methods
-	Stateless
-	Caching
-	Security

### Resources
REST architecture treats every content as a resource. These resources can be Text Files, Html Pages, Images, Videos or Dynamic Business Data. REST Server simply provides access to resources and REST client accesses and modifies the resources. Here each resource is identified by URIs/ Global IDs. REST uses various representations to represent a resource where Text, JSON, XML. The most popular representations of resources are XML and JSON.
Representation of Resources XML, JSON, HTML etc.
  ```
    <user>
    <id>1</id>
    <name>Mahesh</name>
    <profession>Teacher</profession>
    </user>
    {
    "id":1,
    "name":"Mahesh", "profession":"Teacher"
    }
  ```

### Good Resources Representation
REST does not impose any restriction on the format of a resource representation. A client can ask for JSON representation whereas another client may ask for XML representation of the same resource to the server and so on.
Understandability − Both the Server and the Client should be able to understand and utilize the representation format of the resource.

Completeness − Format should be able to represent a resource completely. For example, a resource can contain another resource. Format should be able to represent simple as well as complex structures of resources.

Linkablity − A resource can have a linkage to another resource, a format should be able to handle such situations.

Verb − Indicates the HTTP methods such as GET, POST, DELETE, PUT, etc.

URI − Uniform Resource Identifier (URI) to identify the resource on the server.

HTTP Version − Indicates the HTTP version. For example, HTTP v1.1.

Request Header − Contains metadata for the HTTP Request message as key-value pairs. For example, client (or browser) type, format supported by the client, format of the message body, cache settings, etc.

Request Body − Message content or Resource representation.

Status/Response Code − Indicates the Server status for the requested resource. For example, 404 means resource not found and 200 means response is ok.

HTTP Version − Indicates the HTTP version. For example HTTP v1.1.

Response Header − Contains metadata for the HTTP Response message as key value pairs. For example, content length, content type, response date, server type, etc.

Response Body − Response message content or Resource representation.

### Chrome developer Tools
- Addressing refers to locating a resource or multiple resources lying on the server. It is analogous to locate a postal address of a person.
- Constructing a Standard URI
  - Use Plural Noun − Use plural noun to define resources.

  - Avoid using spaces − Use underscore (_) or hyphen (-) when using a long resource name. For example, use authorized_users instead of authorized%20users.

  - Use lowercase letters − Although URI is case-insensitive, it is a good practice to keep the url in lower case letters only.

  - Maintain Backward Compatibility − As Web Service is a public service, a URI once made public should always be available. In case, URI gets updated, redirect the older URI to a new URI using the HTTP Status code, 300.

- Use HTTP Verb − Always use HTTP Verb like GET, PUT and DELETE to do the operations on the resource. It is not good to use operations name in the URI.

### The following HTTP methods are most commonly used in a REST based architecture.
- GET − Provides a read only access to a resource.
- POST − Used to create a new resource.
- PUT − Used to update an existing resource or create a new resource.
- DELETE − Used to remove a resource.
- OPTIONS − Used to get the supported operations on a resource.

### Statelessness
- As per the REST architecture, a RESTful Web Service should not keep a client state on the server. This restriction is called Statelessness. It is the responsibility of the client to pass its context to the server and then the server can store this context to process the client's further request. For example, session maintained by server is identified by session identifier passed by the client.
  ```
    <book>
    <id>1</id>
    <name>Game of throne</name>
    </book>
  ```
Stateless means every time, you hit the RESTful Service, it should return the same value, regardless the State of the user journey.

### Statelessness Pros vs Cons
- Pros:
  - Web services can treat each method request independently.
  - Web	services	need	not	maintain	the	client's	previous	interactions.	It	simplifies	the application design.
  - As HTTP is itself a statelessness protocol, RESTful Web Services work seamlessly with the HTTP protocols.

- Cons
  - Web services need to get extra information in each request and then interpret to get the client's state in case the client interactions are to be taken care of.

- Solutions
  - Server Side Session, Business Process Engine in the background etc.

Caching refers to storing the server response in the client itself, so that a client need not make a server request for the same resource again and again. A server response should have information about how caching is to be done, so that a client caches the response for a time- period or never caches the server response.

### swagger2 

- 接口非常多，细节又复杂，如果由程序员⾼高质量量的输出一个⽂文档，经常耗时⻓而且效 果也不好，抱怨声不绝与耳。
- 随着时间的推移，文档需要与代码保持同步。但由于大部分程序员都还有着⽂档不重 要的思想，于是总有这样那样的原因导致程序员不愿意或遗忘了了更新文档。

Swagger 是一系列列 RESTful API 的⼯工具，通过 Swagger 可以获得⼀一种交互式⽂档，客户端 SDK 的⾃动⽣成等功能。
Swagger 的⽬标是为 REST APIs 定义⼀个标准的、与语⾔无关的接⼝，使人和计算机在看不到源码或者看不到⽂档或者不能通过⽹络流量检测的情况下，能发现和解各种服务的功能。当服务通过 Swagger 定义，消费者就能与远程的服务互动通过少量的实现逻辑。类似于低级编程接⼝，Swagger去掉了调用服务时的很多猜测。
 
### GraphQL
GraphQL 是⼀一个⽤用于API 的查询语⾔言，是
⼀一个使⽤用基于类型系统来执⾏行行查询的服务端运⾏行行时（类型系统由你的数据定义）。
GraphQL 并没有和任何特定数据库或者存储引擎绑定，⽽而是依靠你现有的代码和数据⽀支撑。

1.	Round-Trips are lesser in GraphQL
2.	Client Specific Queries
3.	Self Discoverable
4.	GraphQL is Hierarchical

### 其他接⼝口通信⽅方式
- RPC：远程过程调⽤用Remote Procedure Call
- Protocol: TCP, HTTP
- Format: xml, JSON, protocol buffer..
- Tools: Thrift, gPRC
