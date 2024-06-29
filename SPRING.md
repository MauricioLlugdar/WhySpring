# What is Spring Framework?

The Spring Framework is lightweight open source project for building enterprise Java Apps. Aims to simplify complexities that come with an enterprise Java apps.

## Core Features

* IoC (Inversion of Control): Provides a streamlined way to configure and manage Java objects. The framework is responsible of the life cycle of the defined Java object. Use Dependency Injection to provide the object reference during runtime.

* AOP (Aspect Oriented Programming): Provide more modularity, login, cashing, authentication, etc.

* DAF (Data Access Framework): Simplifies the database communication proccess, by providing direct support for poppular data access framework in Java, like JDBC, Hibernate, JPA Api.

* MVC: Allow us to easy create projects with the MVC pattern.

## What is an Spring Bean?

An Spring Bean is an object managed(life cycle, org. dependecies) by the Spring Framework. Spring beans could be configure using xml, Java annotations or Java code.
"In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container."

<p>@Qualifier let us tell Spring which bean to inject. If we don't use it, we may have ambiguity problems with the beans</p>
<p>Nevertheless we can use the @Primary annotation to disambiguate and set 1 bean as a primary bean</p>

<a href=https://www.baeldung.com/spring-bean>@Bean and @Qualifier</a>

### Annotations

<p>@Configuration declares class as full configuration class</p>
<p>@Bean declares bean configuration class. If we put @Bean("examplename") now the name for that Bean is examplename instead of the name of the method</p>


``` java
    @Configuration
    class VehicleFactoryConfig {
    	
		@Bean
    	Engine engine() {
        	return new Engine();
    	}
	
	}
```

<p>@Component marks a class as an Spring Component. As a general component annotation indicates that the class should be initialized, configured and managed by the core container</p>
<p>@Repository, @Service and @Controller as meta-annotation for @Component that allows re-fine components</p>
<p>Constructor-dependency injection is automatically done using @Autowired, by injecting the constructor paramenter/s</p>
<p>@Autowired on Constructior is optional if there is only one constructor</p>


### Dependecy Injection(Pattern to implement IoC)

Spring Framework provides 4 ways to inject Beans

* Constructor: During bean construction
* Field(Not recommended, only for test)
* Configuration: Configuration Methods
* Setter: Setter Methods Injection

Example without DI
``` java
	public class Store {
		private Item item;
 
    	public Store() {
    	    item = new ItemImpl1();    
    	}
	}
```
Example with DI (Constructor Injection)
``` java
	public class Store {
    	private Item item;

    	public Store(Item item) { // We dont know the object implementation
        	this.item = item;
    	}
	}
``` 
Example with DI (Method Injection)
``` java
	@Service
	public class DefaultPaymentService{
		@Autowired
		public void configureClass(
			AccountRepository accountRepository,
			FeeCalculator feeCalculator
		){
			// Some fancy code
		}
	}
```
### Bean Scoping

* Bean Scope: Life cycle of a Spring Bean and its availability in the context of the app.

* Multiple scopes:
* Life cycle of a Spring Bean (Managed by the Spring Container)

	<ol>
		<li>SINGLETON: This is the default scope, the Spring Container only creates 1 instance and all requests for that bean name will return the same object. Any modifications to this object will be reflected in all references to the bean</li>
		<li>PROTOTYPE: A bean with prototype scope will return a different instance every time is called. It is defined by setting the value prototype to the @Scope("prototype") annotation</li>
		<li>REQUEST: The bean is created for each HTTP request</li>
		<li>SESSION: The bean is created for each HTTP session</li>
		<li>APPLICATION: Is similar to the Singleton scope. In this case, the same instance of the bean is shared across multiple servlet-based applications running in the same ServletContext, while singleton scoped beans are scoped to a single application context only.</li>
		<li>WEBSOCKET: Similar to Singleton scope but limited to a WebSocket session only</li>
	</ol>

	Example of Application Scope
``` java
	@Bean
	@ApplicationScope
	public HelloMessageGenerator(){
		
		applicationScopedBean() {
		return new HelloMessageGenerato();
		}
	
	}
```